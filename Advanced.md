---
layout: page
title: Features
order: 2.5
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

* `-config`:  Read options from this file 
* `-train_src`:  Path to the training source data 
* `-train_tgt`:  Path to the training target data 
* `-valid_src`:  Path to the validation source data 
* `-valid_tgt`:  Path to the validation target data 
* `-save_data`:  Output file for the prepared data 
* `-src_vocab_size`:  Size of the source vocabulary [50000]
* `-tgt_vocab_size`:  Size of the target vocabulary [50000]
* `-src_vocab`:  Path to an existing source vocabulary 
* `-tgt_vocab`:  Path to an existing target vocabulary 
* `-features_vocabs_prefix`:  Path prefix to existing features vocabularies 
* `-src_seq_length`:  Maximum source sequence length [50]
* `-tgt_seq_length`:  Maximum target sequence length [50]
* `-shuffle`:  Shuffle data [1]
* `-seed`:  Random seed [3435]


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

OpenNMT supports additional features on source and target words in the form of discrete labels.

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

## Training

### Train - Full option list

#### Data options


* `-data`:  Path to the training *-train.t7 file from preprocess.lua 
* `-save_model`:  Model filename (the model will be saved as<save_model>_epochN_PPL.t7 where PPL is the validation perplexity []
* `-train_from`:  If training from a checkpoint then this is the path to the pretrained model. 
* `-continue`:   If training from a checkpoint, whether to continue the training in the same configuration or not. [false]

#### Model options

* `-layers`:  Number of layers in the LSTM encoder/decoder [2]
* `-rnn_size`:  Size of LSTM hidden states [500]
* `-word_vec_size`:  Word embedding sizes [500]
* `-feat_merge`:  Merge action for the features embeddings: concat or sum [concat]
* `-feat_vec_exponent`:  When using concatenation, if the feature takes N valuesthen the embedding dimension will be set to N^exponent [0.7]
* `-feat_vec_size`:  When using sum, the common embedding size of the features [20]
* `-input_feed`:  Feed the context vector at each time step as additional input (via concatenation with the word embeddings) to the decoder. [1]
* `-residual`:  Add residual connections between RNN layers. [false]
* `-brnn`:  Use a bidirectional encoder [false]
* `brnn_merge`:   Merge action for the bidirectional hidden states: concat or sum [sum]


#### Optimization options

* `-max_batch_size`:  Maximum batch size [64]
* `-epochs`:  Number of training epochs [13]
* `-start_epoch`:  If loading from a checkpoint, the epoch from which to start [1]
* `-start_iteration`:  If loading from a checkpoint, the iteration from which to start [1]
* `-param_init`:  Parameters are initialized over uniform distribution with support (-param_init, param_init) [0.1]
* `-optim`:  Optimization method. Possible options are: sgd, adagrad, adadelta, adam [sgd]
* `-learning_rate`:  Starting learning rate. If adagrad/adadelta/adam is used,then this is the global learning rate. Recommended settings are: sgd = 1,adagrad = 0.1, adadelta = 1, adam = 0.0002 [1]
* `-max_grad_norm`:  If the norm of the gradient vector exceeds this renormalize it to have the norm equal to max_grad_norm [5]
* `-dropout`:  Dropout probability. Dropout is applied between vertical LSTM stacks. [0.3]
* `-learning_rate_decay`:  Decay learning rate by this much if (i) perplexity does not decreaseon the validation set or (ii) epoch has gone past the start_decay_at_limit [0.5]
* `-start_decay_at`:  Start decay after this epoch [9]
* `-curriculum`:  For this many epochs, order the minibatches based on sourcesequence length. Sometimes setting this to 1 will increase convergence speed. [0]
* `-pre_word_vecs_enc`:  If a valid path is specified, then this will loadpretrained word embeddings on the encoder side.See README for specific formatting instructions. []
* `-pre_word_vecs_dec`:  If a valid path is specified, then this will loadpretrained word embeddings on the decoder side.See README for specific formatting instructions. []
* `-fix_word_vecs_enc`:  Fix word embeddings on the encoder side [false]
* `fix_word_vecs_dec`:  Fix word embeddings on the decoder side [false]


#### Other options

* `-gpuid`:  1-based identifier of the GPU to use. CPU is used when the option is < 1 [0]
* `-nparallel`:  When using GPUs, how many batches to execute in parallel.Note: this will technically change the final batch size to max_batch_size*nparallel. [1]
* `-async_parallel`:  Use asynchronous parallelism training. [false]
* `-async_parallel_minbatch`:  For async parallel computing, minimal number of batches before being parallel. [1000]
* `-no_nccl`:  Disable usage of nccl in parallel mode. [false]
* `-disable_mem_optimization`:  Disable sharing internal of internal buffers between clones - which is in general safe,except if you want to look inside clones for visualization purpose for instance. [false]
* `-save_every`:  Save intermediate models every this many iterations within an epoch.If = 0, will not save models within an epoch.  [0]
* `-report_every`:  Print stats every this many iterations within an epoch. [50]
* `-seed`:  Seed for random initialization [3435]

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

### Translation - full option list

#### Data options

* `-src`:  Source sequence to decode (one line per sequence) 
* `-tgt`:  True target sequence (optional) 
* `-output`:  Path to output the predictions (each line will be the decoded sequence [pred.txt]
* `-model` :  Path to model .t7 file 


#### Beam Search options


* `-beam_size`:  Beam size [5]
* `-batch_size`:  Batch size [30]
* `-max_sent_length`:  Maximum output sentence length. [250]
* `-replace_unk`:  Replace the generated UNK tokens with the source token thathad the highest attention weight. If phrase_table is provided,it will lookup the identified source token and give the correspondingtarget token. If it is not provided (or the identified source tokendoes not exist in the table) then it will copy the source token [false]
* `-phrase_table`:  Path to source-target dictionary to replace UNKtokens. See README.md for the format this file should be in []
* `-n_best`:  If > 1, it will also output an n_best list of decoded sentences [1]
* `max_num_unks`:   All sequences with more unks than this will be ignored during beam search [inf]

#### Other options

* `-gpuid`:  1-based identifier of the GPU to use. CPU is used when the option is < 1 [0]
* `-fallback_to_cpu`:  If = true, fallback to CPU if no GPU available [false]

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



