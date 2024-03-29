---
layout: page
title: OpenNMT-py models
---

This page lists pretrained models for OpenNMT-py.

* TOC
{:toc}

## Translation

{:.pretrained}
| | New! NLLB 200 3.3B - Transformer ([download](https://s3.amazonaws.com/opennmt-models/nllb-200/nllb-200-3.3B-onmt.pt)) |
| | New! NLLB 200 1.3B - Transformer ([download](https://s3.amazonaws.com/opennmt-models/nllb-200/nllb-200-1.3B-onmt.pt)) |
| | New! NLLB 200 1.3B distilled - Transformer ([download](https://s3.amazonaws.com/opennmt-models/nllb-200/nllb-200-1.3Bdst-onmt.pt)) |
| | New! NLLB 200 600M - Transformer ([download](https://s3.amazonaws.com/opennmt-models/nllb-200/nllb-200-600M-onmt.pt)) |
| --- | --- |
| Configuration | Yaml file example to run inference [inference config](https://s3.amazonaws.com/opennmt-models/nllb-200/nllb-inference.yaml)<br/> Please change the source and terget languages in the yaml |
| Sentence Piece model | [SP Model](https://s3.amazonaws.com/opennmt-models/nllb-200/flores200_sacrebleu_tokenizer_spm.model) |
| Results | cf [Forum](https://forum.opennmt.net/t/nllb-200-with-opennmt-py-the-good-the-bad-and-the-ugly/5151) |

{:.pretrained}
| | New! v3 English-German - Transformer Large ([download](https://s3.amazonaws.com/opennmt-models/v3-py/ende/ende-large-withoutBT.pt)) |
| --- | --- |
| BPE Model | [BPE](https://s3.amazonaws.com/opennmt-models/v3-py/ende/subwords.en_de.bpe) <br/> '{"mode": "aggressive", "joiner_annotate": True, "preserve_placeholders": True, "case_markup": True, "soft_case_regions": True, "preserve_segmented_tokens": True, "segment_case": True, "segment_numbers": True, "segment_alphabet_change": True}' |
| BLEU | newstest2014 = 31.2<br/>newstest2016 = 40.7<br/>newstest2017 = 32.9<br/>newstest2018 = 49.1<br/>newstest2019 = 45.9 |

{:.pretrained}
| | English-German - v2 format model Transformer ([download](https://s3.amazonaws.com/opennmt-models/transformer-ende-wmt-pyOnmt.tar.gz)) |
| --- | --- |
| Configuration | Base Transformer configuration with standard [training options](http://opennmt.net/OpenNMT-py/FAQ.html#how-do-i-use-the-transformer-model-do-you-support-multi-gpu) |
| Data | [WMT](https://s3.amazonaws.com/opennmt-trainingdata/wmt_ende_sp.tar.gz) with shared SentencePiece model<br/>Original Paper replication |
| BLEU | newstest2014 = 26.89<br/>newstest2017 = 28.09 |

{:.pretrained}
| | German-English - 2-layer BiLSTM ([download](https://s3.amazonaws.com/opennmt-models/iwslt-brnn2.s131_acc_62.71_ppl_7.74_e20.pt)) |
| --- | --- |
| Configuration | 2-layer BiLSTM with hidden size 500 trained for 20 epochs |
| Data | [IWSLT '14 DE-EN](https://github.com/pytorch/fairseq/blob/e734b0fa58fcf02ded15c236289b3bd61c4cffdf/data/prepare-iwslt14.sh) |
| BLEU | 30.33 |

## Summarization

### English

{:.pretrained}
| | 2-layer LSTM ([download](https://s3.amazonaws.com/opennmt-models/gigaword_nocopy_acc_51.33_ppl_12.74_e20.pt)) |
| --- | --- |
| Configuration | 2-layer LSTM with hidden size 500 trained for 20 epochs |
| Data | [Gigaword standard](https://github.com/harvardnlp/sent-summary) |
| Gigaword F-Score | R1 = 33.60<br/>R2 = 16.29<br/>RL = 31.45 |

{:.pretrained}
| | 2-layer LSTM with copy attention ([download](https://s3.amazonaws.com/opennmt-models/gigaword_copy_acc_51.78_ppl_11.71_e20.pt)) |
| --- | --- |
| Configuration | 2-layer LSTM with hidden size 500 and copy attention trained for 20 epochs |
| Data | [Gigaword standard](https://github.com/harvardnlp/sent-summary) |
| Gigaword F-Score | R1 = 35.51<br/>R2 = 17.35<br/>RL = 33.17 |

{:.pretrained}
| | Transformer ([download](https://s3.amazonaws.com/opennmt-models/sum_transformer_model_acc_57.25_ppl_9.22_e16.pt)) |
| --- | --- |
| Configuration | See OpenNMT-py [summarization example](http://opennmt.net/OpenNMT-py/Summarization.html) |
| Data | [CNN/Daily Mail](https://github.com/harvardnlp/sent-summary) |

{:.pretrained}
| | 1-layer BiLSTM ([download](https://s3.amazonaws.com/opennmt-models/ada6_bridge_oldcopy_tagged_larger_acc_54.84_ppl_10.58_e17.pt)) |
| --- | --- |
| Configuration | See OpenNMT-py [summarization example](http://opennmt.net/OpenNMT-py/Summarization.html) |
| Data | [CNN/Daily Mail](https://github.com/harvardnlp/sent-summary) |
| Gigaword F-Score | R1 = 39.12<br/>R2 = 17.35<br/>RL = 36.12 |

### Chinese

{:.pretrained}
| | 1-layer BiLSTM ([download](https://s3.amazonaws.com/opennmt-models/lcsts_acc_56.86_ppl_10.97_e11.pt)) |
| --- | --- |
| Author | [playma](https://github.com/playma) |
| Configuration | **Preprocessing options:** src_vocab_size 8000, tgt_vocab_size 8000, src_seq_length 400, tgt_seq_length 30, src_seq_length_trunc 400, tgt_seq_length_trunc 100.<br/>**Training options:** 1 layer, LSTM 300, WE 500, encoder_type brnn, input feed, AdaGrad, adagrad_accumulator_init 0.1, learning_rate 0.15, 30 epochs |
| Data | [LCSTS](http://icrc.hitsz.edu.cn/Article/show/139.html) |
| Gigaword F-Score | R1 = 35.67<br/>R2 = 23.06<br/>RL = 33.14 |

## Dialog

{:.pretrained}
| | 2-layer LSTM ([download](https://s3.amazonaws.com/opennmt-models/dialog_acc_39.74_ppl_26.63_e13.pt)) |
| --- | --- |
| Configuration | 2 layers, LSTM 500, WE 500, input feed, dropout 0.2, global_attention mlp, start_decay_at 7, 13 epochs |
| Data | [OpenSubtitles](http://opus.lingfil.uu.se/download.php?f=OpenSubtitles/en.tar.gz) |
