---
layout: page
title: OpenNMT-tf models
---

This page lists pretrained models for OpenNMT-tf.

## Translation

{:.pretrained}
| | English-German - Transformer ([checkpoint](https://s3.amazonaws.com/opennmt-models/averaged-ende-ckpt500k.tar.gz), [SavedModel](https://s3.amazonaws.com/opennmt-models/averaged-ende-export500k.tar.gz)) |
| --- | --- |
| Configuration | Base Transformer configuration with standard [training options](https://github.com/OpenNMT/OpenNMT-tf/tree/master/scripts/wmt) |
| Data | [WMT](https://s3.amazonaws.com/opennmt-trainingdata/wmt_ende_sp.tar.gz) with shared SentencePiece model |
| BLEU | newstest2014 = 26.9<br/>newstest2017 = 28.0 |
