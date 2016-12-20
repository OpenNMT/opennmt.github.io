
Models that we have trained using OpenNMT


* [English -> German](https://s3.amazonaws.com/opennmt-models/onmt_baseline_wmt15-all.en-de_epoch13_7.19.t7)

Coming Soon

* German -> English 
* Summarization (Gigaword) 

## Benchmarks

This page benchmarks training results of open-source NMT systems with generated models of OpenNMT and other systems.

## English-German - WMT15

Training data from [WMT15 - Translation Task](http://www.statmt.org/wmt15/translation-task.html).

| Who/When      | Corpus Prep     | Training Tool | Training Parameters | Server Details | Training Time/Memory | Scores | Model |
|:------------- |:--------------- |:-------------|:-------------------|:---------------|:-------------|:------|:-----|
| 2016/20/12<br>Baseline | <small>+ Raw Europarl v7<br>+ Common Crawl<br>+ News Commentary v10<hr>OpenNMT `aggressive` tokenization<hr>OpenNMT `preprocess.lua` default option (50k vocab, 50 max sent, shuffle) | OpenNMT `111f16a` | default options:<br>2 layers, RNN 500, WE 500, input feed<br>13 epochs | <small>Intel(R) Core(TM) i7-6800K CPU @ 3.40GHz, 256Gb Mem, GPU 4xTITAN X (Pascal) | 355 min/epoch, 2.5Gb GPU usage | newstest2014 (cleaned):<br>NIST=5.5376<br>BLEU=0.1702 | 692M [here](https://s3.amazonaws.com/opennmt-models/onmt_baseline_wmt15-all.en-de_epoch13_7.19.t7) |

If you have a competitive model - please contact us at info@opennmt.net with necessary information to reproduce, and we will register your system in this "hall of fame".
