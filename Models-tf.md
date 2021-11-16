---
layout: page
title: OpenNMT-tf models
---

This page lists pretrained models for OpenNMT-tf.

## Translation

{:.pretrained}
| | English-German - Transformer |
| --- | --- |
| Downloads | [checkpoint](https://s3.amazonaws.com/opennmt-models/averaged-ende-ckpt500k.tar.gz), [SavedModel (TensorFlow 1.x)](https://s3.amazonaws.com/opennmt-models/averaged-ende-export500k.tar.gz), [SavedModel (TensorFlow 2.x)](https://s3.amazonaws.com/opennmt-models/averaged-ende-export500k-v2.tar.gz) |
| Configuration | Base Transformer configuration with standard [training options](https://github.com/OpenNMT/OpenNMT-tf/tree/master/scripts/wmt) |
| Data | [WMT](https://s3.amazonaws.com/opennmt-trainingdata/wmt_ende_sp.tar.gz) with shared SentencePiece model |
| BLEU | newstest2014 = 26.9<br/>newstest2017 = 28.0 |


| | Argos Open Tech translate models (English from/to several languages)  - Transformer |
| --- | --- |
| Downloads | https://www.argosopentech.com/argospm/index/ (CTranslate2 models) |
| Configuration |Transformer model with SetencePiece tokenizer |
| BLEU | Different BLEU scores depending on the model |


| | Softcatalà production ready models from Catalan to multiple languages (English, German, etc)  - Transformer |
| --- | --- |
| Downloads | https://github.com/Softcatala/nmt-models (CTranslate2 and TensorFlow models) |
| Configuration |TransformerRelative model with SentencePiece tokenizer |
| Data | https://github.com/Softcatala/parallel-catalan-corpus |
| BLEU | Different BLEU scores depending on the model |
