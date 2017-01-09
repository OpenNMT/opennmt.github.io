---
layout: page
title: Guide
order: 2
---

* TOC
{:toc}

## Installation

OpenNMT only requires a vanilla <a href="http://torch.ch/docs/getting-started.html">Torch</a> install. It makes use of the libraries: nn, nngraph, and cunn. We highly recommend use of GPU-based training.

Alternatively there is a <a href="https://hub.docker.com/r/harvardnlp/opennmt/">Docker image</a> available.

## Quickstart

OpenNMT consists of three commands:

1) Preprocess the data.

```th preprocess.lua -train_src data/src-train.txt -train_tgt data/tgt-train.txt -valid_src data/src-val.txt -valid_tgt data/tgt-val.txt -save_data data/demo```

2) Train the model.

```th train.lua -data data/demo-train.t7 -save_model model [-gpuid 1]```

3) Translate sentences.

```th translate.lua -model model_final.t7 -src data/src-val.txt [-gpuid 1]```

Let's walk through each of these commands in more detail. 


### Step 1: Preprocess Data

```th preprocess.lua -train_src data/src-train.txt -train_tgt data/tgt-train.txt -valid_src data/src-val.txt -valid_tgt data/tgt-val.txt -save_data data/demo```

The `preprocess.lua` command can also take additional <a href="http://opennmt.net/OpenNMT/details/preprocess/">options</a>.  

Here we are working with example data in `data/` folder.
The data consists of a source (`src`) and target (`tgt`) data.
This will take the source/target train/valid files (`src-train.txt, tgt-train.txt,
src-val.txt, tgt-val.txt`). There is one sentence per line, and words are space separated (the corpus is said "tokenized" - see <a href="https://github.com/OpenNMT/OpenNMT/tree/master/tools#tokenizationdetokenization">here</a> if your own corpus is not yet tokenized).

* data/tgt-train.txt

```
Es geht nicht an , dass über Ausführungsbestimmungen , deren Inhalt , Zweck und Ausmaß vorher nicht bestimmt ist , zusammen mit den nationalen Bürokratien das Gesetzgebungsrecht des Europäischen Parlaments ausgehebelt wird .
Meistertrainer und leitender Dozent des italienischen Fitnessverbands für Aerobic , Gruppenfitness , Haltungsgymnastik , Stretching und Pilates; arbeitet seit 2004 bei Antiche Terme als Personal Trainer und Lehrer für Stretching , Pilates und Rückengymnastik .
Also kam ich nach Südafrika " , erzählte eine Frau namens Grace dem Human Rights Watch-Mitarbeiter Gerry Simpson , der die Probleme der zimbabwischen Flüchtlinge in Südafrika untersucht .
```

* data/src-train.txt

```
It is not acceptable that , with the help of the national bureaucracies , Parliament &apos;s legislative prerogative should be made null and void by means of implementing provisions whose content , purpose and extent are not laid down in advance .
Federal Master Trainer and Senior Instructor of the Italian Federation of Aerobic Fitness , Group Fitness , Postural Gym , Stretching and Pilates; from 2004 , he has been collaborating with Antiche Terme as personal Trainer and Instructor of Stretching , Pilates and Postural Gym .
&quot; Two soldiers came up to me and told me that if I refuse to sleep with them , they will kill me . They beat me and ripped my clothes .
```

After running the system will build the following files:

* `demo.src.dict`: Dictionary of source vocab to index mappings.
* `demo.tgt.dict`: Dictionary of target vocab to index mappings.
* `demo-train.t7`: serialized Torch file containing vocabulary, training and validation data

The `*.dict` files are needed to check vocabulary, or to preprocess data with fixed vocabularies.
These files are simple human-readable dictionaries.

* data/demo.src.dict

```
<blank> 1
<unk> 2
<s> 3
</s> 4
It 5
is 6
not 7
acceptable 8
that 9
, 10
with 11
```

Internally the system never touches the words themselves, but uses these indices.

### Step 2: Train the model

```th train.lua -data data/demo-train.t7 -save_model demo-model
```

The main train command is quite simple. Minimally it takes a data file
and a save file.  This will run the default model, which consists of a
2-layer LSTM with 500 hidden units on both the encoder/decoder. You
can also add `-gpuid 1` to use (say) GPU 1.

The `train.lua` command can take many additional <a
href="http://opennmt.net/OpenNMT/details/train/">options</a>
describing the desired model size and structure as
well as the training procedure and initialization.


### Step 3: Translate

```th translate.lua -model demo-model_final.t7 -src data/src-val.txt [-gpuid 1]
```

Now you have a model which you can use to predict on new data. We do this by running beam search.

This will output predictions into `pred.txt`. The predictions are going to be quite terrible,
as the demo dataset is small. Try running on some larger datasets! For example you can download
millions of parallel sentences for [translation](http://www.statmt.org/wmt15/translation-task.html)
or [summarization](https://github.com/harvardnlp/sent-summary).

The `translate.lua` command can take  more <a
href="http://opennmt.net/OpenNMT/details/translate/">options</a>
describing the beam search procedure.

## Additional System Features

### Configuration files

When using the main scripts `preprocess.lua`, `train.lua` and `translate.lua`, you can pass your options using a configuration file. The file has a simple key-value syntax with one `option = value` per line. Here is an example:

```
$ cat generic.txt
rnn_size = 600
layers = 4
brnn = true
save_model = generic
```

It handles empty lines and ignores lines prefixed with `#`.

You can then pass this file along other options on the command line:

```
th train.lua -config generic.txt -data data/demo-train.t7 -gpuid 1
```

If an option appears both in the file and on the command line, the file takes priority.

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

### Training From Snapshots

As training translation models can take a long time (sometimes many
weeks), OpenNMT supports resuming a model from a snapshot. By default,
it will save a snapshot every epoch, but this can by altered with the
`-save_every` option. Snapshots are fast to save, but can be quite
large. To resume from a snapshot use the `-train_from` option with
the starting snapshot. By default the system will train starting from 
parameter using newly passed in options. To override this, and 
continue from the previous location use the `-continue` option.

### Parallel training

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

### Translation and Beam Search

By default translation is done using beam search. The `-beam_size`
option can be used to trade-off translation time and search accuracy,
with `-beam_size 1` giving greedy search. The small default beam size
is often enough in practice. Beam search can also be used to provide
an approximate n-best list of translations by setting `-n_best`
greater than 1. For analysis, the translation command also takes an
oracle/gold `-tgt` file and will output a comparison of scores.


### Translating UNK Words 

The default translation mode allows the model to produce the UNK
symbol when it is not sure of the specific target word. Often times
UNK symbols will correspond to proper names that can be directly
transposed between languages. The `-replace_unk` option will
substitute UNK with a source word using the attention of the
model. Alternatively, advanced users may prefer to provide a
preconstructed phrase table from an external aligner (such as
fast_align) using the `-phrase_table` option to allow for non-
identity replacement.

## Tools


### Tokenization


To tokenize a corpus:

```
th tools/tokenize.lua OPTIONS < file > file.tok
```

This additionally requires `bit32` for Lua < 5.2

where the options are:

* `-mode`: can be `aggressive` or `conservative` (default). In conservative mode, letters, numbers and '_' are kept in sequence, hyphens are accepted as part of tokens. Finally inner characters `[.,]` are also accepted (url, numbers).
* `-sep_annotate`: if set, add reversible separator mark to indicate separator-less or BPE tokenization (preference on symbol, then number, then letter)
* `-case_feature`: generate case feature - and convert all tokens to lowercase
  * `N`: not defined (for instance tokens without case)
  * `L`: token is lowercased (opennmt)
  * `U`: token is uppercased (OPENNMT)
  * `C`: token is capitalized (Opennmt)
  * `M`: token case is mixed (OpenNMT)
* `-bpe_model`: when set, activate BPE using the BPE model filename

Note:

* `￨` is the feature separator symbol - if such character is used in source text, it is replace by its non presentation form `│`
* `￭` is the separator mark (generated in `-sep_annotate marker` mode) - if such character is used in source text, it is replace by its non presentation form `■`


If you activate `sep_annotate` marker, the tokenization is reversible - just use:

```
th tools/detokenize.lua [-case_feature] < file.tok > file.detok
```



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


## Extending the System (Image-to-Text)

OpenNMT is explicitly separated out into a library and application 
section. All modeling and training code can be directly used within
other Torch applications. 

As an example use case we have released an extension for translating
from images-to-text. This model replaces the source-side word
embeddings with a convolutional image network. The full model is
available at <a href="https://github.com/opennmt/im2text">OpenNMT/im2text</a>.


  
