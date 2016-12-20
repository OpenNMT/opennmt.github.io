---
layout: page
title: Models
order: 3
---

## Pretrained


Available models trained using OpenNMT

* [English -> German](https://s3.amazonaws.com/opennmt-models/onmt_baseline_wmt15-all.en-de_epoch13_7.19.t7)
* [German -> English](https://s3.amazonaws.com/opennmt-models/onmt_baseline_wmt15-all.de-en_epoch13_8.98.t7)

More models coming soon

* FR,ES,PT,IT,RO<>FR,ES,PT,IT,RO
* Summarization (Gigaword)

## Benchmarks

This page benchmarks training results of open-source NMT systems with generated models of OpenNMT and other systems.
If you have a competitive model - please contact us at info@opennmt.net with necessary information to reproduce, and we will register your system in this "hall of fame".


### English->German

| Who/When      | Corpus Prep     | Training Tool | Training Parameters | Server Details | Training Time/Memory | Scores | Model |
|:------------- |:--------------- |:-------------|:-------------------|:---------------|:-------------|:------|:-----|
| 2016/20/12<br>Baseline | [WMT15 - Translation Task](http://www.statmt.org/wmt15/translation-task.html)<br><small>+ Raw Europarl v7<br>+ Common Crawl<br>+ News Commentary v10<br>OpenNMT `aggressive` tokenization<br>OpenNMT `preprocess.lua` default option (50k vocab, 50 max sent, shuffle) | OpenNMT `111f16a` | default options:<br>2 layers, RNN 500, WE 500, input feed<br>13 epochs | <small>Intel(R) Core(TM) i7-6800K CPU @ 3.40GHz, 256Gb Mem, trained on 1 GPU TITAN X (Pascal) | 355 min/epoch, 2.5Gb GPU usage | valid newstest2013:<br>PPL: 7.19<br>newstest2014 (cleaned):<br>NIST=5.5376<br>BLEU=0.1702 | 692M [here](https://s3.amazonaws.com/opennmt-models/onmt_baseline_wmt15-all.en-de_epoch13_7.19.t7) |

### German->English

| Who/When      | Corpus Prep     | Training Tool | Training Parameters | Server Details | Training Time/Memory | Scores | Model |
|:------------- |:--------------- |:-------------|:-------------------|:---------------|:-------------|:------|:-----|
| 2016/20/12<br>Baseline | [WMT15 - Translation Task](http://www.statmt.org/wmt15/translation-task.html)<br><small>+ Raw Europarl v7<br>+ Common Crawl<br>+ News Commentary v10<br>OpenNMT `aggressive` tokenization<br>OpenNMT `preprocess.lua` default option (50k vocab, 50 max sent, shuffle) | OpenNMT `111f16a` | default options:<br>2 layers, RNN 500, WE 500, input feed<br>13 epochs | <small>Intel(R) Core(TM) i7-6800K CPU @ 3.40GHz, 256Gb Mem, trained on 1 GPU TITAN X (Pascal) | 346 min/epoch, 2.5Gb GPU usage | valid newstest2013:<br>PPL: 8.98<br>newstest2014 (cleaned):<br>NIST=6.4531<br>BLEU=0.2067 | 692M [here](https://s3.amazonaws.com/opennmt-models/onmt_baseline_wmt15-all.de-en_epoch13_8.98.t7) |
