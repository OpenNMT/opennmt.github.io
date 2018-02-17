---
layout: page
title: PyTorch Models
order: 3
---

## Pretrained


Available models trained using OpenNMT.

* [English Summarization](https://lstm.seas.harvard.edu/latex/opennmt-py-models/model_acc_51.33_ppl_12.74_e20.pt)
* [German to English Translation for IWSLT '14](http://lstm.seas.harvard.edu/latex/opennmt-py-models/baseline-brnn2.s131_acc_62.71_ppl_7.74_e20.pt)

## Benchmarks

This page benchmarks training results of open-source NMT systems with generated models of OpenNMT and other systems.

### English Summarization

| Who/When      | Corpus Prep     | Training Tool | Training Parameters | Server Details | Training Time/Memory | Scores | Model |
|:------------- |:--------------- |:-------------|:-------------------|:---------------|:-------------|:------|:-----|
| 2018/02/11<br>Baseline | [Gigaword Standard](https://github.com/harvardnlp/sent-summary) | OpenNMT `d4ab35a` | default options:<br>2 layers, RNN 500, WE 500, input feed<br>20 epochs | <small>Trained on 1 GPU TITAN X  |  | Gigaword F-Score R1: 33.60 R2: 16.29 RL: 31.45  | 331MB [here](http://lstm.seas.harvard.edu/latex/opennmt-py-models/model_acc_51.33_ppl_12.74_e20.pt) |
| 2018/02/11<br>Baseline | [IWSLT '14 DE-EN](https://github.com/facebookresearch/fairseq-py/blob/master/data/prepare-iwslt14.sh) | OpenNMT `d4ab35a` | default options:<br>2 layers, RNN 500, WE 500, input feed<br>20 epochs | <small>Trained on 1 GPU TITAN X  |  | BLEU Score: 30.33 | 203MB [here](http://lstm.seas.harvard.edu/latex/opennmt-py-models/baseline-brnn2.s131_acc_62.71_ppl_7.74_e20.pt) |
