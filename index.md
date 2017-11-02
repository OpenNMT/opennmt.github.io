---
layout: page
title: Home
order: 1
---

[OpenNMT](http://opennmt.net/) is an open source (MIT) initiative for neural machine translation and neural sequence modeling.

<center style="padding: 40px"><img width="80%" src="http://opennmt.github.io/simple-attn.png" /></center>

Since its launch in December 2016, OpenNMT has become a collection of implementations targeting both academia and industry. The systems are designed to be simple to use and easy to extend, while maintaining efficiency and state-of-the-art accuracy.

**OpenNMT has currently 3 main implementations:**

* [OpenNMT-lua](https://github.com/OpenNMT/OpenNMT) (a.k.a. OpenNMT): the original project developed with [LuaTorch](http://torch.ch).<br/>Full-featured, optimized, and stable code ready for quick experiments and production.
* [OpenNMT-py](https://github.com/OpenNMT/OpenNMT-py): an OpenNMT-lua clone using the more modern [PyTorch](http://pytorch.org).<br/>Initially created by the Facebook AI research team as an example, this implementation is easier to extend and particularly suited for research.
* [OpenNMT-tf](https://github.com/OpenNMT/OpenNMT-tf): a [TensorFlow](https://www.tensorflow.org/) alternative.<br/>The more recent project focusing on large scale experiments and high performance model serving using the latest TensorFlow features.

All versions are currently maintained.

**Common features include:**

* Simple general-purpose interface, requiring only source/target files.
* Highly configurable models and training procedures.
* Recent research features to improve system performance.
* Extensions to allow other sequence generation tasks such as summarization, image-to-text, or speech-recognition.
* Active <a href="http://forum.opennmt.net">community</a> welcoming both academic and industrial requests and contributions.
