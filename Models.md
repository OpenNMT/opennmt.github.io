---
layout: page
title: Torch Models
order: 3
---

Available models trained using OpenNMT.

### English-German Translation

| Corpus | Tokenization | Model | BLEU score | |
| --- | --- | --- | --- | --- |
| [WMT 17](http://www.statmt.org/wmt17/translation-task.html) | `-mode aggressive -segment_case -joiner_annotate` | 2 layers, 1024 hidden size, 32K shared BPE | *newstest2017*: 25.1 | [download](https://s3.amazonaws.com/opennmt-models/wmt-ende_l2-h1024-bpe32k_release.tar.gz) |
| [WMT 17](http://www.statmt.org/wmt17/translation-task.html) (with back-translation) | `-mode aggressive -segment_case -joiner_annotate` | 2 layers, 1024 hidden size, 32K shared BPE | *newstest2016*: 32.8 | [download](https://s3.amazonaws.com/opennmt-models/wmt-ende-with-bt_l2-h1024-bpe32k_release.tar.gz) |

### Multi-way Translation (FR,ES,PT,IT,RO<>FR,ES,PT,IT,RO)

| Corpus | Tokenization | Model | |
| --- | --- | --- |
| [Multi](https://s3.amazonaws.com/opennmt-trainingdata/multi-esfritptro-parallel-tokenized.tgz) | `-mode aggressive` | 4 layers, 1000 hidden size,<br>600 embedding size, brnn<br>32K shared BPE | [download](https://s3.amazonaws.com/opennmt-models/onmt_esfritptro-4-1000-600_epoch13_3.12_release_v2.t7) |

More details on the [forum](http://forum.opennmt.net/t/training-romance-multi-way-model/86).

### English Summarization

| Corpus | Model | Score | |
| --- | --- | --- | --- |
| [Gigaword standard](https://github.com/harvardnlp/sent-summary) | 2 layers, 500 hidden size,<br>500 embedding size, 11 epochs | R1: 33.13<br>R2: 16.09<br> RL: 31.00 | [download](https://s3.amazonaws.com/opennmt-models/textsum_epoch7_14.69_release.t7) |
