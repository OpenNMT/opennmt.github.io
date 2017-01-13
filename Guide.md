---
layout: page
title: Quickstart
order: 2
---

* TOC
{:toc}

## Installation

OpenNMT only requires a vanilla <a href="http://torch.ch/docs/getting-started.html">Torch</a> install. It makes use of the libraries: nn, nngraph, cunn and bit32. We highly recommend use of GPU-based training.

Alternatively there is a <a href="https://hub.docker.com/r/harvardnlp/opennmt/">Docker image</a> available.

## Quickstart

OpenNMT consists of three steps. (These steps assume you data is already tokenized. If not see the tokenization section below.)


1) Preprocess the data.

```th preprocess.lua -train_src data/src-train.txt -train_tgt data/tgt-train.txt -valid_src data/src-val.txt -valid_tgt data/tgt-val.txt -save_data data/demo```

2) Train the model.

```th train.lua -data data/demo-train.t7 -save_model model [-gpuid 1]```

3) Translate sentences.

```th translate.lua -model model_final.t7 -src data/src-val.txt -output file-tgt.tok [-gpuid 1]```

Let's walk through each of these commands in more detail. 

### Step 1: Preprocess Data

```th preprocess.lua -train_src data/src-train.txt -train_tgt data/tgt-train.txt -valid_src data/src-val.txt -valid_tgt data/tgt-val.txt -save_data data/demo```

Here we are working with example data in `data/` folder.
The data consists of a source (`src`) and target (`tgt`) data.
This will take the source/target train/valid files (`src-train.txt, tgt-train.txt,
src-val.txt, tgt-val.txt`). 

Get the full options list on the <a href="http://opennmt.net//Advanced/#preprocess---full-option-list">features page</a>.

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

Get the full options list on the <a href="http://opennmt.net//Advanced/#train---full-option-list">features page</a>.


### Step 3: Translate

```th translate.lua -model demo-model_final.t7 -src data/src-val.txt -output file-tgt.tok [-gpuid 1]
```

Now you have a model which you can use to predict on new data. We do this by running beam search.

This will output predictions into `file-tgt.tok`. The predictions are going to be quite terrible,
as the demo dataset is small. Try running on some larger datasets! For example you can download
millions of parallel sentences for [translation](http://www.statmt.org/wmt15/translation-task.html)
or [summarization](https://github.com/harvardnlp/sent-summary).

Get the full options list on the <a href="http://opennmt.net//Advanced/#translation---full-option-list">features page</a>.


## Tokenization 

Our demo data comes pre-tokenized. If you data is not tokenized, we also provide a simple language-independent tokenizer/detokenizer that we have found to be effective for machine translation tasks. You can run the tokenizer with the following commands:


1) Tokenize your data (file is src-train.txt, tgt-train.txt, valid and test sets as well)

```th tools/tokenize.lua -joiner_annotate < file > file.tok```

The tokenize.lua scripts can also handle following options:

* `-mode`: can be `aggressive` or `conservative` (default). In conservative mode, letters, numbers and '_' are kept in sequence, hyphens are accepted as part of tokens. Finally inner characters `[.,]` are also accepted (url, numbers).
* `-case_feature`: generate case feature - and convert all tokens to lowercase

Get the full options list on the <a href="http://opennmt.net//Advanced/#tokenizer---full-option-list">features page</a>.

2) Detokenize the output.

```th tools/detokenize.lua < file-tgt.tok > file-tgt.detok```
