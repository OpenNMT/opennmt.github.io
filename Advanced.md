---
layout: page
title: Advanced guide
order: 2.5
---

* TOC
{:toc}

## Configuration files

When using the main scripts `preprocess.lua`, `train.lua` and `translate.lua`, you can pass your options using a configuration file. The file has a simple key-value syntax with one `option = value` per line. Here is an example:

```
$ cat generic.txt
rnn_size = 600
layers = 4
brnn = true
save_model = generic
```

It handles empty line and ignore lines prefixed with `#`.

You can then pass this file along other options on the command line:

```
th train.lua -config generic.txt -data data/demo-train.t7 -gpuid 1
```

If an option appears both in the file and on the command line, the file takes priority.

## Data Preparation

### Word features

OpenNMT supports additional features on source and target words in the form of **discrete labels**.

* On the source side, these features act as additional information to the encoder. An
embedding will be optimized for each label and then fed as additional source input
alongside the word it annotates.
* On the target side, these features will be predicted by the network. The
decoder is then able to decode a sentence and annotate each word.

To use additional features, directly modify your data by appending labels to each word with
the special character `￨` (unicode character FFE8). There can be an arbitrary number of additional
features in the form `word￨feat1￨feat2￨...￨featN` but each word must have the same number of
features and in the same order. Source and target data can have a different number of additional features.

As an example, see `data/src-train-case.txt` which uses a separate feature
to represent the case of each word. Using case as a feature is a way to optimize the word
dictionary (no duplicated words like "the" and "The") and gives the system an additional
information that can be useful to optimize its objective function.

```
it￨C is￨l not￨l acceptable￨l that￨l ,￨n with￨l the￨l help￨l of￨l the￨l national￨l bureaucracies￨l ,￨n parliament￨C &apos;s￨l legislative￨l prerogative￨l should￨l be￨l made￨l null￨l and￨l void￨l by￨l means￨l of￨l implementing￨l provisions￨l whose￨l content￨l ,￨n purpose￨l and￨l extent￨l are￨l not￨l laid￨l down￨l in￨l advance￨l .￨n
```

You can generate this case feature with OpenNMT's tokenization script and the `-case_feature` flag.

#### Vocabulary

By default, features vocabulary size is unlimited. Depending on the type of features you are using, you may want to limit their vocabulary during the preprocessing with the `-src_vocab_size` and `-tgt_vocab_size` options in the format `word_size[,feat1_size[,feat2_size[...]]]`. For example:

```
# unlimited source features vocabulary size
-src_vocab_size 50000

# first feature vocabulary is limited to 60, others are unlimited
-src_vocab_size 50000,60

# second feature vocabulary is limited to 100, others are unlimited
-src_vocab_size 50000,0,100

# limit vocabulary size of the first and second feature
-src_vocab_size 50000,60,100
```

## Training

### Pre-trained embeddings

When training with small amounts of data, performance can be improved
by starting with pretrained embeddings. The arguments
`-pre_word_vecs_dec` and `-pre_word_vecs_enc` can be used to specify
these files. The pretrained embeddings must be manually constructed
torch serialized matrices that correspond to the src and tgt
dictionary files. By default these embeddings will be updated during
training, but they can be held fixed using `-fix_word_vecs_enc` and
`-fix_word_vecs_dec`.

### Word features embeddings

The feature embedding size is automatically computed based on the number of values the feature takes. The default size reduction works well for features with few values like the case or POS. For other features, you may want to manually choose the embedding size with the `src_word_vec_size` and `-tgt_word_vec_size` options. They behave similarly to `-src_vocab_size` with a comma-separated list of embedding size: `word_vec_size[,feat1_vec_size[,feat2_vec_size[...]]]`.

By default each embedding is concatenated. You can choose to sum them by setting `-feat_merge sum`. Note that in this case each feature embedding must have the same dimension. You can set the common embedding size with `-feat_vec_size`.

### Multi-GPU training

OpenNMT supports *data parallelism* during the training. This technique allows the use of several GPUs by training batches in parallel on different *network replicas*. To enable this option, assign a list of comma-separated GPU identifier to the `-gpuid` option. For example:

```
th train.lua -data data/demo-train.t7 -save_model demo -gpuid 1,2,4
```

will use the first, the second and the fourth GPU of the machine.

There are 2 different modes:

* **synchronous parallelism** (default): in this mode, each replica processes in parallel a different batch at each iteration. The gradients from each replica are accumulated, and parameters updated and synchronized. Note that when using `N` GPU(s), the actual batch size is `N * max_batch_size`.
* **asynchronous parallelism** (`-async_parallel` flag): in this mode, the different replicas are independently
calculating their own gradient, updating a master copy of the parameters and getting updated values
of the parameters. Note that a GPU core is dedicated to storage of the master copy of the parameters and is not used for training. Also, to enable convergence at the beginning of the training, only one replica is working for the first `-async_parallel_minbatch` iterations.

### Training from a saved model

By default, OpenNMT saves a checkpoint at the end of every epoch. For more frequent saves, you can use the `-save_every` option which defines the number of iterations after which the training saves a checkpoint.

There are several reasons one may want to train from a saved model with the `-train_from` option:

* continuing a stopped training
* continuing the training with a smaller batch size
* training a model on new data (incremental adaptation)
* starting a training from pre-trained parameters
* etc.

#### Resuming a stopped training

It is common that a training stops: crash, server reboot, user action, etc. In this case, you may want to continue the training for more epochs by using using the `-continue` option. For example:

```
# start the initial training
th train.lua -gpuid 1 -data data/demo-train.t7 -save_model demo -save_every 50

# train for several epochs...

# need to reboot the server!

# continue the training from the last checkpoint
th train.lua -gpuid 1 -data data/demo-train.t7 -save_model demo -save_every 50 -train_from demo_checkpoint.t7 -continue
```

The `-continue` flag ensures that the training continues with the same configuration and optimization states.

#### Training from pre-trained parameters

Another use case it to use a base model and train it further with new training options (in particular the optimization method and the learning rate). Using `-train_from` without `-continue` will start a new training with parameters initialized from a pre-trained model.

*Note that the model topology and dropout value can not be changed during a retraining.*


## Translation

### Translation and beam search

By default translation is done using beam search. The `-beam_size`
option can be used to trade-off translation time and search accuracy,
with `-beam_size 1` giving greedy search. The small default beam size
is often enough in practice. Beam search can also be used to provide
an approximate n-best list of translations by setting `-n_best`
greater than 1. For analysis, the translation command also takes an
oracle/gold `-tgt` file and will output a comparison of scores.


### Translating unknown words

The default translation mode allows the model to produce the UNK
symbol when it is not sure of the specific target word. Often times
UNK symbols will correspond to proper names that can be directly
transposed between languages. The `-replace_unk` option will
substitute UNK with a source word using the attention of the
model.

Alternatively, advanced users may prefer to provide a
preconstructed phrase table from an external aligner (such as
fast_align) using the `-phrase_table` option to allow for non-identity replacement.
Instead of copying the source token with the highest attention, it will
lookup in the phrase table for a possible translation. If a valid replacement
is not found then the source token will be copied.

The phrase table is a file with one translation per line in the format:

```
source|||target
```

Where `source` and `target` are **case sensitive** and **single** tokens.


### Releasing models

After training a model, you may want to release it for inference only by using the `release_model.lua` script. A released model takes less space on disk and is compatible with CPU translation.

```
th tools/release_model.lua -model model.t7 -gpuid 1
```

By default, it will create a `model_release.t7` file. See `th tools/release_model.lua -h` for advanced options.

### C++ translator

OpenNMT also includes an optimized C++-only <a href="https://github.com/opennmt/ctranslate">translator</a> for CPU deployment. The code has no dependencies on Torch or Lua and can be run out of the box with standard OpenNMT models. Simply follow the CPU instructions above to release the model, and then use the [installation instructions](https://github.com/opennmt/ctranslate).

The C++ version takes the same arguments as `translate.lua`.

```cli/translate --model model_release.t7 --src src-val.txt
```

### Translation Server

OpenNMT includes a translation server for running translate remotely. This also is an
easy way to use models from other languages such as Java and Python. 

The server uses the 0MQ for RPC. You can install 0MQ and the Lua bindings on Ubuntu by running:

```
sudo apt-get install libzmq-dev
luarocks install json
luarocks install lua-zmq ZEROMQ_LIBDIR=/usr/lib/x86_64-linux-gnu/ ZEROMQ_INCDIR=/usr/include
```

Also you will need to install the OpenNMT as a library.

```
luarocks make rocks/opennmt-scm-1.rockspec
```

The translation server can be run using any of the arguments from `translate.lua`. 

```
th tools/translation_server.lua -host ... -port ... -model ...
```

**Note:** the default host is set to `127.0.0.1` which only allows local access. If you want to support remote access, use `0.0.0.0` instead.

It runs as a message queue that takes in a JSON batch of src sentences. For example the following 5 lines of Python
code can be used to send a single sentence for translation.

```python
import zmq, sys, json
sock = zmq.Context().socket(zmq.REQ)
sock.connect("tcp://127.0.0.1:5556")
sock.send(json.dumps([{"src": " ".join(sys.argv[1:])}]))
print sock.recv()
```

For a longer example, see our <a href="http://github.com/OpenNMT/Server/">Python/Flask server</a> in development. 


##  Extending the system (Image-to-Text)

OpenNMT is explicitly separated out into a library and application 
section. All modeling and training code can be directly used within
other Torch applications. 

As an example use case we have released an extension for translating
from images-to-text. This model replaces the source-side word
embeddings with a convolutional image network. The full model is
available at <a href="https://github.com/opennmt/im2text">OpenNMT/im2text</a>.



