---
layout: page
title: Frequently asked questions
order: 4
---

* TOC
{:toc}


## General

### Why should I use OpenNMT?

OpenNMT has been successfully used in [many research and industry applications](/publications). It is now a robust and complete ecosystem for machine translation and related tasks.

Here are some reasons to use OpenNMT:

* The 2 supported implementations, [OpenNMT-py](https://github.com/OpenNMT/OpenNMT-py) and [OpenNMT-tf](https://github.com/OpenNMT/OpenNMT-tf), give the choice between [PyTorch](https://pytorch.org/) and [TensorFlow](https://www.tensorflow.org/) which are 2 of the most popular deep learning toolkits.
* The implementations are packed with [many configurable models and features](/features) including for other generation tasks: summarization, speech to text, image to text, etc.
* The [OpenNMT ecosystem](https://github.com/OpenNMT) includes tools and projects to cover the full NMT workflow:
  * [CTranslate2](https://github.com/OpenNMT/CTranslate2), a fast inference engine for OpenNMT models which explores model quantization and inference acceleration on CPU and GPU
  * [Tokenizer](https://github.com/OpenNMT/Tokenizer), a fast and customizable text tokenization library
* The NMT systems are able to reach high translation quality and speed, on par with the best online translation offerings.
* You get reactive and free support on the [community forum](http://forum.opennmt.net/).

### Who is behind OpenNMT?

OpenNMT is currently supported by the companies [SYSTRAN](http://www.systransoft.com/) and [Ubiqus](https://www.ubiqus.com/). The main maintainers are:

* [Guillaume Klein](https://github.com/guillaumekln) (SYSTRAN)
* [Vincent Nguyen](https://github.com/vince62s) (Ubiqus)
* [Jean Senellart](https://github.com/jsenellart) (SYSTRAN)

The project was initiated in December 2016 by the [Harvard NLP](https://nlp.seas.harvard.edu/) group and SYSTRAN.

### Which OpenNMT implementation should I use?

OpenNMT has 2 main implementations: [OpenNMT-py](https://github.com/OpenNMT/OpenNMT-py) and [OpenNMT-tf](https://github.com/OpenNMT/OpenNMT-tf).

You first need to decide between [PyTorch](https://pytorch.org/) and [TensorFlow](https://www.tensorflow.org/). Both frameworks have strengths and weaknesses, see which one is more suited and easier for you to integrate.

Then, each OpenNMT implementation has its own design and set of [unique features](/features). For example OpenNMT-py has better support for other tasks (summarization, speech, image) and is generally faster while OpenNMT-tf supports modular architectures and language modeling. See their respective GitHub repository for more details.

### How to cite the OpenNMT project?

If you are using the project for academic work, please cite the initial [system demonstration paper](https://www.aclweb.org/anthology/P17-4012) for ACL 2017:

```
@inproceedings{klein-etal-2017-opennmt,
    title = "{O}pen{NMT}: Open-Source Toolkit for Neural Machine Translation",
    author = "Klein, Guillaume  and
      Kim, Yoon  and
      Deng, Yuntian  and
      Senellart, Jean  and
      Rush, Alexander",
    booktitle = "Proceedings of {ACL} 2017, System Demonstrations",
    month = jul,
    year = "2017",
    address = "Vancouver, Canada",
    publisher = "Association for Computational Linguistics",
    url = "https://www.aclweb.org/anthology/P17-4012",
    pages = "67--72",
}
```

### Where can I get support?

The [OpenNMT forum](http://forum.opennmt.net/) is the place to go for asking general questions or requesting support. You can usually expect a reply within 1 or 2 work days.

For bugs, please report them on the GitHub repositories directly.

### Where can I go to learn about NMT?

We recommend starting with the [ACL'16 NMT](https://sites.google.com/site/acl16nmt/home) produced by researchers at Stanford and NYU. The tutorial also includes a detailed bibliography describing work in the field.

## Requirements

### What do I need to train a NMT model?

You just need two files: a source file and a target file, each with one sentence per line with words that are space separated. These files can come from standard free translation corpora such a [WMT](http://www.statmt.org/wmt19/), or it can be any other sources you want to train from.

### What type of computer do I need to train with?

While in theory you can train on any machine, in practice for all but trivally small data sets you will need a GPU if you want the training to finish in a reasonable amount of time.

We recommend using a NVIDIA GPU with at least 8GB of memory.

## Models

### How can I replicate the full-scale NMT translation results?

We published a [baseline training script](https://github.com/OpenNMT/OpenNMT-tf/tree/master/scripts/wmt) to train a robust German-English translation model using OpenNMT-tf. If you are using OpenNMT-py, you can apply the same preprocessing and train a Transformer model with the [recommended options](http://opennmt.net/OpenNMT-py/FAQ.html#how-do-i-use-the-transformer-model-do-you-support-multi-gpu).

### Are there pretrained translation models that I can try?

There are several pretrained models available for [OpenNMT-py](/Models-py) and [OpenNMT-tf](/Models-tf).

### Where can I get training data for translation?

Try the [OPUS](http://opus.lingfil.uu.se/) project, an open-source collection of parallel corpora. After stripping XML tags, you should be able to use the raw files directly in OpenNMT.

### I am interested in other seq2seq-like problems such as summarization, dialogue, tree-generation. Can OpenNMT work for these?

Yes. OpenNMT is a general-purpose attention-based sequence to sequence system. There is very little code that is translation specific, and so it should be effective for many of these applications.

For the case of summarization, OpenNMT has been shown to be more effective than neural systems like [NAMAS](https://github.com/facebook/NAMAS), and will be supported going forward. See the [OpenNMT-py models](/Models-py) page for a pretrained summarization system on the Gigaword dataset.

### I am interested in variants of seq2seq such as image-to-text generation. Can OpenNMT work for these?

Yes. OpenNMT-py includes a relatively general-purpose [im2text](http://opennmt.net/OpenNMT-py/im2text.html) system, with a small amount of additional code. Feel free to use this as a model for extending OpenNMT.
