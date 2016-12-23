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

```th preprocess.lua -train_src data/src-train.txt -train_tgt data/tgt-train.txt -valid_src data/src-val.txt -valid_tgt data/tgt-val.txt -output data/demo```

2) Train the model.

```th train.lua -data data/demo-train.t7 -save_model model```

3) Translate sentences.

```th evaluate.lua -model model_final.t7 -src data/src-val.txt -src_dict data/demo.src.dict -tgt_dict data/demo.tgt.dict```

Let's walk through each of these commands in more detail. 


### Step 1: Preprocess Data

```th preprocess.lua -train_src data/src-train.txt -train_tgt data/tgt-train.txt -valid_src data/src-val.txt -valid_tgt data/tgt-val.txt -output data/demo```

The `preprocess.lua` command can also take additional <a href="https://opennmt.github.io/OpenNMT/Options#preprocess">options</a>.  

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
href="https://opennmt.github.io/OpenNMT/Options#train">options</a>
describing the desired model size and structure as
well as the training procedure and initialization.


### Step 3: Translate

```th translate.lua -model demo-model_final.t7 -src data/src-val.txt  -src_dict data/demo.src.dict -tgt_dict data/demo.tgt.dict
```

Now you have a model which you can use to predict on new data. We do this by running beam search.

This will output predictions into `pred.txt`. The predictions are going to be quite terrible,
as the demo dataset is small. Try running on some larger datasets! For example you can download
millions of parallel sentences for [translation](http://www.statmt.org/wmt15/translation-task.html)
or [summarization](https://github.com/harvardnlp/sent-summary).

The `evaluate.lua` command can take  more <a
href="https://opennmt.github.io/OpenNMT/Options#evaluate">options</a>
describing the beam search procedure.

## Additional Features

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
`words-|-feat1-|-feat2...` using the special symbol `-|-`.

As an example, consider the data in `data/src-train-case.txt` which uses a separate features to represent the case of each word. 

* data/src-train-case.txt

```
it-|-C is-|-l not-|-l acceptable-|-l that-|-l ,-|-n with-|-l the-|-l help-|-l of-|-l the-|-l national-|-l bureaucracies-|-l ,-|-n parliament-|-C &apos;s-|-l legislative-|-l prerogative-|-l should-|-l be-|-l made-|-l null-|-l and-|-l void-|-l by-|-l means-|-l of-|-l implementing-|-l provisions-|-l whose-|-l content-|-l ,-|-n purpose-|-l and-|-l extent-|-l are-|-l not-|-l laid-|-l down-|-l in-|-l advance-|-l .-|-n
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


### Deploying Models

It is often important to train models using a GPU, but may be
necessary to deploy them on a standard CPU system. We provide a script
`release_model.lua` to convert trained models to work in CPU mode. 

```th release_model.lua -model demo-model_final.t7 -output_model demo-cpu.t7 
```

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

## Extending the System (Image-to-Text)

OpenNMT is explicitly separated out into a library and application 
section. All modeling and training code can be directly used within
other Torch applications. 

As an example use case we have released an extension for translating
from images-to-text. This model replaces the source-side word
embeddings with a convolutional image network. The full model is
available at <a href="https://github.com/opennmt/im2text">OpenNMT/im2text</a>.


  
