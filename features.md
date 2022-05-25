---
layout: page
title: Features
---

While OpenNMT initially focused on standard sequence to sequence models applied to machine translation, it has been extended to support many additional models and features. The tables below highlight some of the key features of each implementation.

* TOC
{:toc}

## Tasks

| | OpenNMT-py | OpenNMT-tf |
| --- | :---: | :---: |
| Image to text | ✓ (v1 only) | |
| Language modeling | ✓ | ✓ |
| Sequence classification | | ✓ |
| Sequence tagging | | ✓ |
| Sequence to sequence | ✓ | ✓ |
| Speech to text | ✓ (v1 only) | ✓ |
| Summarization | ✓ | |

## Models

| | OpenNMT-py | OpenNMT-tf |
| --- | :---: | :---: |
| [ConvS2S](https://arxiv.org/abs/1705.03122) | ✓ | |
| [DeepSpeech2](https://arxiv.org/abs/1512.02595v1) | ✓ (v1 only) | |
| [GPT-2](https://d4mucfpksywv.cloudfront.net/better-language-models/language-models.pdf) | ✓ | ✓ |
| [Im2Text](https://arxiv.org/abs/1609.04938) | ✓ (v1 only) | |
| [Listen, Attend and Spell](https://arxiv.org/abs/1508.01211) | | ✓ |
| [RNN with attention](https://arxiv.org/abs/1508.04025) | ✓ | ✓ |
| [Transformer](https://arxiv.org/abs/1706.03762) | ✓ | ✓ |

## Model configuration

| | OpenNMT-py | OpenNMT-tf |
| --- | :---: | :---: |
| Cascaded and multi-column encoder | | ✓ |
| [Copy attention](https://arxiv.org/abs/1603.06393) | ✓ | |
| [Coverage attention](https://arxiv.org/abs/1601.04811) | ✓ | |
| Hybrid models | | ✓ |
| Multiple source | | ✓ |
| Multiple input features | ✓ | ✓ |
| [Relative position representations](https://arxiv.org/abs/1803.02155) | ✓ | ✓ |
| Tied embeddings | ✓ | ✓ |

## Training

| | OpenNMT-py | OpenNMT-tf |
| --- | :---: | :---: |
| Automatic evaluation | ✓ | ✓ |
| Automatic model export | | ✓ |
| [Contrastive learning](https://ai.google/research/pubs/pub48253/) | | ✓ |
| Data augmentation (e.g. noise) | ✓ | ✓ |
| Early stopping | ✓ | ✓ |
| Gradient accumulation | ✓ | ✓ |
| Supervised alignment | ✓ | ✓ |
| Mixed precision | ✓ | ✓ |
| Moving average | ✓ | ✓ |
| Multi-GPU | ✓ | ✓ |
| Multi-node | ✓ | ✓ |
| On-the-fly tokenization | ✓ | ✓ |
| Pretrained embeddings | ✓ | ✓ |
| [Scheduled sampling](https://arxiv.org/abs/1506.03099) | | ✓ |
| Sentence weighting | | ✓ |
| Vocabulary update | ✓ | ✓ |
| Weighted dataset | ✓ | ✓ |

## Decoding

| | OpenNMT-py | OpenNMT-tf |
| --- | :---: | :---: |
| Beam search | ✓ | ✓ |
| [Coverage penalty](https://arxiv.org/abs/1609.08144) | ✓ | ✓ |
| [CTranslate2 compatibility](https://github.com/OpenNMT/CTranslate2) | ✓ | ✓ |
| Ensemble | ✓ | |
| [Length penalty](https://arxiv.org/abs/1609.08144) | ✓ | ✓ |
| N-best rescoring | ✓ | ✓ |
| N-gram blocking | ✓ | |
| Phrase table | ✓ | |
| [Random noise](https://arxiv.org/abs/1808.09381) | ✓ | ✓ |
| Random sampling | ✓ | ✓ |
| Replace unknown | ✓ | ✓ |

For more details on how to use these features, please refer to the documentation of each project:

* [OpenNMT-py](https://opennmt.net/OpenNMT-py)
* [OpenNMT-tf](https://opennmt.net/OpenNMT-tf)
