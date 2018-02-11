---
layout: page
title: PyTorch Models
order: 3
---

## Pretrained


Available models trained using OpenNMT.

* [English Summarization](https://lstm.seas.harvard.edu/latex/opennmt-py-models/model_acc_51.33_ppl_12.74_e20.pt)

## Benchmarks

This page benchmarks training results of open-source NMT systems with generated models of OpenNMT and other systems.
If you have a competitive model - please contact us at info@opennmt.net with necessary information to reproduce, and we will register your system in this "hall of fame".

### English Summarization

| Who/When      | Corpus Prep     | Training Tool | Training Parameters | Server Details | Training Time/Memory | Scores | Model |
|:------------- |:--------------- |:-------------|:-------------------|:---------------|:-------------|:------|:-----|
| 2018/02/11<br>Baseline | [Gigaword Standard](https://github.com/harvardnlp/sent-summary) | OpenNMT `d4ab35a` | default options:<br>2 layers, RNN 500, WE 500, input feed<br>20 epochs | <small>Trained on 1 GPU TITAN X  |  | Gigaword F-Score R1: 33.60 R2: 16.29 RL: 31.45  | 331MB [here](https://lstm.seas.harvard.edu/latex/opennmt-py-models/model_acc_51.33_ppl_12.74_e20.pt) |
