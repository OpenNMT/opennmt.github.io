---
layout: page
title: Features
order: 6
---

* TOC
{:toc}


## Data Preparation

### Tokenizer - full option list

* `-mode`: can be `aggressive` or `conservative` (default). In conservative mode, letters, numbers and '_' are kept in sequence, hyphens are accepted as part of tokens. Finally inner characters `[.,]` are also accepted (url, numbers).
* `-joiner_annotate`: if set, add joiner marker to indicate separator-less or BPE tokenization. The marker is defined by `-joiner` option and by default is joined to tokens (preference on symbol, then number, then letter) but can be independent if `-joiner_new` option is set.
* `-joiner`: default (￭) - the joiner marker
* `-joiner_new`: if set, the joiner is an independent token
* `-case_feature`: generate case feature - and convert all tokens to lowercase
  * `N`: not defined (for instance tokens without case)
  * `L`: token is lowercased (opennmt)
  * `U`: token is uppercased (OPENNMT)
  * `C`: token is capitalized (Opennmt)
  * `M`: token case is mixed (OpenNMT)
* `-bpe_model`: when set, activate BPE using the BPE model filename

Note:

* `￨` is the feature separator symbol - if such character is used in source text, it is replace by its non presentation form `│`
* `￭` is the default joiner marker (generated in `-joiner_annotate` mode) - if such character is used in source text, it is replace by its non presentation form `■`

### Preprocess - full option list


config
:   Read options from this file []

train_src
:   Path to the training source data []

train_tgt
:   Path to the training target data []

valid_src
:   Path to the validation source data []

valid_tgt
:   Path to the validation target data []

save_data
:   Output file for the prepared data []

src_vocab_size
:   Size of the source vocabulary [50000]

tgt_vocab_size
:   Size of the target vocabulary [50000]

src_vocab
:   Path to an existing source vocabulary []

tgt_vocab
:   Path to an existing target vocabulary []

features_vocabs_prefix
:   Path prefix to existing features vocabularies []

src_seq_length
:   Maximum source sequence length [50]

tgt_seq_length
:   Maximum target sequence length [50]

shuffle
:   Shuffle data [1]

seed
:   Random seed [3435]



### Pre-trained Embeddings

When training with small amounts of data, performance can be improved
by starting with pretrained embeddings. The arguments
`-pre_word_vecs_dec` and `-pre_word_vecs_enc` can be used to specify
these files. The pretrained embeddings must be manually constructed
torch serialized matrices that correspond to the src and tgt
dictionary files. By default these embeddings will be updated during
training, but they can be held fixed using `-fix_word_vecs_enc` and
`-fix_word_vecs_dec`.

### Word Features

OpenNMT supports including additional features on source and target
words.  These features are are given their embeddings which are
concatenated (or summed depending on `-feat_merge` argument) upon input, and generated (independently) on
the decoder side. To specify features, simply modify the training data
before the preprocessing step, replacing `word` with
`words￨feat1￨feat2...` using the special symbol `￨` (unicode character FFE8).

As an example, consider the data in `data/src-train-case.txt` which uses a separate features to represent the case of each word. 

* data/src-train-case.txt

```
it￨C is￨l not￨l acceptable￨l that￨l ,￨n with￨l the￨l help￨l of￨l the￨l national￨l bureaucracies￨l ,￨n parliament￨C &apos;s￨l legislative￨l prerogative￨l should￨l be￨l made￨l null￨l and￨l void￨l by￨l means￨l of￨l implementing￨l provisions￨l whose￨l content￨l ,￨n purpose￨l and￨l extent￨l are￨l not￨l laid￨l down￨l in￨l advance￨l .￨n
```

## Training

### Train - Full option list



### Training From Snapshots

As training translation models can take a long time (sometimes many
weeks), OpenNMT supports resuming a model from a snapshot. By default,
it will save a snapshot every epoch, but this can by altered with the
`-save_every` option. Snapshots are fast to save, but can be quite
large. To resume from a snapshot use the `-train_from` option with
the starting snapshot. By default the system will train starting from 
parameter using newly passed in options. To override this, and 
continue from the previous location use the `-continue` option.

### Parallel Training

To accelerate training, you can use *data parallelism* for the training.
Data parallelism is the possibility to use several GPUs for training with parallel
batches on different *replicas*. To enable this option use `-nparallel` option which requires
availability of as many GPU cores. There are 2 different modes:

* synchronous parallelism: in this mode (default), each replica process in parallel a different batch
at each iteration. The gradients from each replica are accumulated, and parameters
updated and synchronized.
* asynchronous parallelism: in this mode (activated with `-async_parallel`, the different replicas are independently
calculating their own gradient, updating a master copy of the parameters and getting updated values
of the parameters.
Note that a GPU core is dedicated to storage of the master copy of the parameters and is not used
for training. Also, to enable convergence at the beginning of the training, only one replica is working for
the first `async_parallel_minbatch` iterations.

To select a subset of the GPUs available on your machine, you should use the `CUDA_VISIBLE_DEVICES` environment variable.
For example, if you want to use the first and last GPU on a 4-GPU server:

```
CUDA_VISIBLE_DEVICES=0,3 th train.lua -gpuid 1 -nparallel 2 -data data/demo-train.t7 -save_model demo
```

Here, GPU 0 will be seen as the first GPU for the process and GPU 3 the second.
Note that `CUDA_VISIBLE_DEVICES` is 0-indexed while `-gpuid` is 1-indexed.


## Translation

### Translation and Beam Search

By default translation is done using beam search. The `-beam_size`
option can be used to trade-off translation time and search accuracy,
with `-beam_size 1` giving greedy search. The small default beam size
is often enough in practice. Beam search can also be used to provide
an approximate n-best list of translations by setting `-n_best`
greater than 1. For analysis, the translation command also takes an
oracle/gold `-tgt` file and will output a comparison of scores.


### Translating Unknown Words

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


### CPU Translation

After training a model on the GPU, you may want to release it to run on the CPU with the `release_model.lua` script.

```
th tools/release_model.lua -model model.t7 -gpuid 1
```

By default, it will create a `model_release.t7` file. See `th tools/release_model.lua -h` for advanced options.

### C++ Translator

OpenNMT also includes an optimized C++-only <a href="https://github.com/opennmt/ctranslate">translator</a> for CPU deployment. The code has no dependencies on Torch or Lua and can be run out of the box with standard OpenNMT models. Simply follow the CPU instructions above to release the model, and then use the installation instructions at https://github.com/opennmt/ctranslate.

The C++ version takes the same arguments as `translate.lua`.

```./translate -src -model model_release.t7 -src src-val.txt
```

### Translation Server

OpenNMT includes a translation server for running translate remotely. This also is an
easy way to use models from other languages such as Java and Python. 

The server uses the 0MQ for RPC. You can install 0MQ and the Lua bindings on Ubuntu by running:

```
sudo apt-get install libzmq-dev
luarocks install https://raw.github.com/Neopallium/lua-zmq/master/rockspecs/lua-zmq-scm-1.rockspec  ZEROMQ_LIBDIR=/usr/lib/x86_64-linux-gnu/ ZEROMQ_INCDIR=/usr/include
```

Also you will need to install the OpenNMT as a library.

```
luarocks make rocks/opennmt-scm-1.rockspec
```

The translation server can be run using any of the arguments from `translate.lua`. 

```
th tools/translation_server.lua -port ... -model ...
```

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


##  Extending the System (Image-to-Text)

OpenNMT is explicitly separated out into a library and application 
section. All modeling and training code can be directly used within
other Torch applications. 

As an example use case we have released an extension for translating
from images-to-text. This model replaces the source-side word
embeddings with a convolutional image network. The full model is
available at <a href="https://github.com/opennmt/im2text">OpenNMT/im2text</a>.



