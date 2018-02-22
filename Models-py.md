---
layout: page
title: PyTorch Models
order: 3
---

## Pretrained


Available models trained using OpenNMT.

* [German to English](http://lstm.seas.harvard.edu/latex/opennmt-py-models/translate/de-en/baseline-brnn2.s131_acc_62.71_ppl_7.74_e20.pt)
* [English Summarization](http://lstm.seas.harvard.edu/latex/opennmt-py-models/summary/model-copy_acc_51.78_ppl_11.71_e20.pt)
* [Dialog System](http://lstm.seas.harvard.edu/latex/opennmt-py-models/dialog/model_acc_39.74_ppl_26.63_e13.pt)

## Benchmarks

This page benchmarks training results of open-source NMT systems with generated models of OpenNMT and other systems.

### German->English

| Who/When      | Corpus Prep     | Training Tool | Training Parameters | Server Details | Training Time/Memory | Translate Parameters | Scores | Model |
|:------------- |:--------------- |:-------------|:-------------------|:---------------|:-------------|:------------|:------|:-----|
| 2018/02/11<br>Baseline | [IWSLT '14 DE-EN](https://github.com/facebookresearch/fairseq-py/blob/master/data/prepare-iwslt14.sh) | OpenNMT `d4ab35a` | 2 layers, RNN 500, WE 500, input feed<br>20 epochs | <small>Trained on 1 GPU TITAN X  |  | | BLEU Score: 30.33 | 203MB [here](http://lstm.seas.harvard.edu/latex/opennmt-py-models/translate/de-en/baseline-brnn2.s131_acc_62.71_ppl_7.74_e20.pt) |

### English Summarization

| Who/When      | Corpus Prep     | Training Tool | Training Parameters | Server Details | Training Time/Memory | Translate Parameters | Scores | Model |
|:------------- |:--------------- |:-------------|:-------------------|:---------------|:-------------|:------------|:------|:-----|
| 2018/02/11<br>Baseline | [Gigaword Standard](https://github.com/harvardnlp/sent-summary) | OpenNMT `d4ab35a` | 2 layers, RNN 500, WE 500, input feed<br>20 epochs | <small>Trained on 1 GPU TITAN X  |  | | Gigaword F-Score R1: 33.60 R2: 16.29 RL: 31.45  | 331MB [here](http://lstm.seas.harvard.edu/latex/opennmt-py-models/summary/model_acc_51.33_ppl_12.74_e20.pt) |
| 2018/02/22<br>Baseline | [Gigaword Standard](https://github.com/harvardnlp/sent-summary) | OpenNMT `338b3b1` | 2 layers, RNN 500, WE 500, input feed, copy_attn, reuse_copy_attn<br>20 epochs | <small>Trained on 1 GPU TITAN X  |  | replace_unk | Gigaword F-Score R1: 35.51 R2: 17.35 RL: 33.17  | 331MB [here](http://lstm.seas.harvard.edu/latex/opennmt-py-models/summary/model-copy_acc_51.78_ppl_11.71_e20.pt) |

### Dialog System

| Who/When      | Corpus Prep     | Training Tool | Training Parameters | Server Details | Training Time/Memory | Translate Parameters | Scores | Model |
|:------------- |:--------------- |:-------------|:-------------------|:---------------|:-------------|:------------|:------|:-----|
| 2018/02/22<br>Baseline | [Opensubtitles](http://opus.lingfil.uu.se/download.php?f=OpenSubtitles/en.tar.gz) | OpenNMT `338b3b1` | 2 layers, RNN 500, WE 500, input feed, dropout 0.2, global_attention mlp, start_decay_at 7<br>13 epochs | <small>Trained on 1 GPU TITAN X  |  | | TBD  | 173MB [here](http://lstm.seas.harvard.edu/latex/opennmt-py-models/dialog/model_acc_39.74_ppl_26.63_e13.pt) |
