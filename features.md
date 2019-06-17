---
layout: page
title: Features
---

While OpenNMT initialy focused on standard sequence to sequence models applied to machine translation, it has been extended to support many additional models and features. The tables below highlight some of the key features of each implementation.

* TOC
{:toc}

## Tasks

| | OpenNMT-py | OpenNMT-tf |
| --- | :---: | :---: |
| Image to text | ✓ | |
| Language modeling | | ✓ |
| Sequence classification | | ✓ |
| Sequence tagging | | ✓ |
| Sequence to sequence | ✓ | ✓ |
| Speech to text | ✓ | ✓ |
| Summarization | ✓ | |

## Models

| | OpenNMT-py | OpenNMT-tf |
| --- | :---: | :---: |
| [ConvS2S](https://arxiv.org/abs/1705.03122) | ✓ | |
| [DeepSpeech2](https://arxiv.org/abs/1512.02595v1) | ✓ | |
| [GPT-2](https://d4mucfpksywv.cloudfront.net/better-language-models/language-models.pdf) | | ✓ |
| [Im2Text](https://arxiv.org/abs/1609.04938) | ✓ | |
| [Listen, Attend and Spell](https://arxiv.org/abs/1508.01211) | | ✓ |
| [RNN with attention](https://arxiv.org/abs/1508.04025) | ✓ | ✓ |
| [Transformer](https://arxiv.org/abs/1706.03762) | ✓ | ✓ |

## Model configuration

| | OpenNMT-py | OpenNMT-tf |
| --- | :---: | :---: |
| [Copy attention](https://arxiv.org/abs/1603.06393) | ✓ | |
| [Coverage attention](https://arxiv.org/abs/1601.04811) | ✓ | |
| Hybrid models | | ✓ |
| Multi source | | ✓ |
| [Relative position representations](https://arxiv.org/abs/1803.02155) | ✓ | |
| Tied embeddings | ✓ | ✓ |

## Training

| | OpenNMT-py | OpenNMT-tf |
| --- | :---: | :---: |
| Automatic evaluation | ✓ | ✓ |
| Early stopping | ✓ | |
| Gradient accumulation | ✓ | ✓ |
| [Guided alignment](https://arxiv.org/abs/1607.01628) | | ✓ |
| Mixed precision | ✓ | ✓ |
| Moving average | ✓ | |
| Multi GPU | ✓ | ✓ |
| Pretrained embeddings | ✓ | ✓ |
| [Scheduled sampling](https://arxiv.org/abs/1506.03099) | | ✓ |
| Vocabulary update | | ✓ |

## Decoding

| | OpenNMT-py | OpenNMT-tf |
| --- | :---: | :---: |
| Beam search | ✓ | ✓ |
| [Coverage penalty](https://arxiv.org/abs/1609.08144) | ✓ | ✓ |
| Ensemble | ✓ | |
| [Length penalty](https://arxiv.org/abs/1609.08144) | ✓ | ✓ |
| N-best rescoring | ✓ | ✓ |
| N-gram blocking | ✓ | |
| Phrase table | ✓ | |
| [Random noise](https://arxiv.org/abs/1808.09381) | | ✓ |
| Random sampling | ✓ | ✓ |
| Replace unknown | ✓ | ✓ |

For more details on how to use these features, please refer to the documentation of each project:

* [OpenNMT-py](http://opennmt.net/OpenNMT-py)
* [OpenNMT-tf](http://opennmt.net/OpenNMT-tf)
