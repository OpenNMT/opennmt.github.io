---
layout: page
title: Models and Recipes
order: 3
---

## Pretrained


Available models trained using OpenNMT

* [English -> German](https://s3.amazonaws.com/opennmt-models/onmt_baseline_wmt15-all.en-de_epoch13_7.19_release.t7)
* [German -> English](https://s3.amazonaws.com/opennmt-models/onmt_baseline_wmt15-all.de-en_epoch13_8.98_release.t7)
* [English Summarization](https://s3.amazonaws.com/opennmt-models/sum_model_epoch11_14.62.t7)
* [Multi-way - FR,ES,PT,IT,RO<>FR,ES,PT,IT,RO](https://s3.amazonaws.com/opennmt-models/onmt_esfritptro-4-1000-600_epoch13_3.12_release.t7)

More models coming soon:

* Ubuntu Dialogue Dataset
* Syntactic Parsing
* Image-to-Text

## Tutorials and Recipes

We provide <a href="http://forum.opennmt.net/c/tutorials">tutorials</a> for training these and other models in our forum.

Additonally, we plan on posting the scripts for each of our <a href="https://github.com/opennmt/recipes">training recipes</a>. 

## Benchmarks

This page benchmarks training results of open-source NMT systems with generated models of OpenNMT and other systems.
If you have a competitive model - please contact us at info@opennmt.net with necessary information to reproduce, and we will register your system in this "hall of fame".


### English->German


| Who/When      | Corpus Prep     | Training Tool | Training Parameters | Server Details | Training Time/Memory | Scores | Model |
|:------------- |:--------------- |:-------------|:-------------------|:---------------|:-------------|:------|:-----|
| 2016/20/12<br>Baseline | [WMT15 - Translation Task](http://www.statmt.org/wmt15/translation-task.html)<br><small>+ Raw Europarl v7<br>+ Common Crawl<br>+ News Commentary v10<br>OpenNMT `aggressive` tokenization<br>OpenNMT `preprocess.lua` default option (50k vocab, 50 max sent, shuffle) | OpenNMT `111f16a` | default options:<br>2 layers, RNN 500, WE 500, input feed<br>13 epochs | <small>Intel(R) Core(TM) i7-6800K CPU @ 3.40GHz, 256Gb Mem, trained on 1 GPU TITAN X (Pascal) | 355 min/epoch, 2.5Gb GPU usage | valid newstest2013:<br>PPL: 7.19<br>newstest2014 (cleaned):<br>NIST=5.5376<br>BLEU=0.1702 | 692M [here](https://s3.amazonaws.com/opennmt-models/onmt_baseline_wmt15-all.en-de_epoch13_7.19_release.t7) |

WMT15 training and validation data also available [here](https://s3.amazonaws.com/opennmt-trainingdata/wmt15-de-en.tgz).

### German->English

| Who/When      | Corpus Prep     | Training Tool | Training Parameters | Server Details | Training Time/Memory | Scores | Model |
|:------------- |:--------------- |:-------------|:-------------------|:---------------|:-------------|:------|:-----|
| 2016/20/12<br>Baseline | [WMT15 - Translation Task](http://www.statmt.org/wmt15/translation-task.html)<br><small>+ Raw Europarl v7<br>+ Common Crawl<br>+ News Commentary v10<br>OpenNMT `aggressive` tokenization<br>OpenNMT `preprocess.lua` default option (50k vocab, 50 max sent, shuffle) | OpenNMT `111f16a` | default options:<br>2 layers, RNN 500, WE 500, input feed<br>13 epochs | <small>Intel(R) Core(TM) i7-6800K CPU @ 3.40GHz, 256Gb Mem, trained on 1 GPU TITAN X (Pascal) | 346 min/epoch, 2.5Gb GPU usage | valid newstest2013:<br>PPL: 8.98<br>newstest2014 (cleaned):<br>NIST=6.4531<br>BLEU=0.2067 | 692M [here](https://s3.amazonaws.com/opennmt-models/onmt_baseline_wmt15-all.de-en_epoch13_8.98_release.t7) |

WMT15 training and validation data also available [here](https://s3.amazonaws.com/opennmt-trainingdata/wmt15-de-en.tgz).

### Multi-way - FR,ES,PT,IT,RO<>FR,ES,PT,IT,RO

Following [Toward Multilingual Neural Machine Translation with Universal Encoder and Decoder (Thanh-Le Ha et al, 2016)](https://arxiv.org/abs/1611.04798) and [Google's Multilingual Neural Machine Translation System: Enabling Zero-Shot Translation (Johnson et al, 2016)](https://arxiv.org/abs/1611.04558) we trained a multi-way engine between French, Spanish, Portuguese, Italian and Romanian.

The corpus used is completely parallel - and there are only 200,000 sentences per language - the tokenized corpus with test, valid is [here](https://s3.amazonaws.com/opennmt-trainingdata/multi-esfritptro-parallel-tokenized.tgz).

| Who/When      | Corpus Prep     | Training Tool | Training Parameters | Server Details | Training Time/Memory | Scores | Model |
|:------------- |:--------------- |:-------------|:-------------------|:---------------|:-------------|:------|:-----|
| 2017/07/01<br>Baseline | OpenNMT `aggressive` tokenization with BPE 32k | OpenNMT `481b784` | 4 layers, RNN 1000, WE 600, input feed, brnn<br>13 epochs | <small>Intel(R) Core(TM) i7-5930K CPU @ 3.50GHz, 96Gb Mem, trained on 1 GPU 1080 GeForce (Pascal) | 887 min/epoch, 6Gb GPU usage | (described in forum) | 2.9G (GPU) [here](https://s3.amazonaws.com/opennmt-models/onmt_esfritptro-4-1000-600_epoch13_3.12_release.t7) |

### English Summarization

| Who/When      | Corpus Prep     | Training Tool | Training Parameters | Server Details | Training Time/Memory | Scores | Model |
|:------------- |:--------------- |:-------------|:-------------------|:---------------|:-------------|:------|:-----|
| 2016/21/12<br>Baseline | [Gigaword Standard](https://github.com/harvardnlp/sent-summary) | OpenNMT `111f16a` | default options:<br>2 layers, RNN 500, WE 500, input feed<br>11 epochs | <small>Trained on 1 GPU TITAN X  |  | Gigaword F-Score R1: 33.13 R2: 16.09 RL: 31.00  | 572M [here](https://s3.amazonaws.com/opennmt-models/sum_model_epoch11_14.62.t7) or [cpu release](https://s3.amazonaws.com/opennmt-models/textsum_epoch7_14.69_release.t7)|

