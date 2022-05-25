---
layout: index
title: Home
order: 1
---

**OpenNMT** is an open source ecosystem for neural machine translation and neural sequence learning.

<center><img width="80%" src="/simple-attn.png" /></center>

Started in December 2016 by the [Harvard NLP](https://nlp.seas.harvard.edu/) group and [SYSTRAN](https://www.systransoft.com/), the project has since been used in [several research and industry applications](/publications). It is currently maintained by [SYSTRAN](https://www.systransoft.com/) and [Ubiqus](https://www.ubiqus.com/).

**OpenNMT provides implementations in 2 popular deep learning frameworks:**

<p>
    <div class="cards" id="cards-primary">
        <div class="card">
            <a class="card-main" title="See on GitHub" href="https://github.com/OpenNMT/OpenNMT-py">
                <img src="public/pytorch.png" alt="PyTorch"/>
                <div class="project"><strong>OpenNMT-py</strong></div>
                <p>User-friendly and multimodal, benefiting from PyTorch ease of use.</p>
            </a>
            <ul>
                <li><a href="/OpenNMT-py">Documentation</a></li>
                <li><a href="/Models-py">Pretrained models</a></li>
            </ul>
        </div>
        <div class="card">
            <a class="card-main" title="See on GitHub" href="https://github.com/OpenNMT/OpenNMT-tf">
                <img src="public/tensorflow.png" alt="TensorFlow"/>
                <div class="project"><strong>OpenNMT-tf</strong></div>
                <p>Modular and stable, powered by the TensorFlow ecosystem.</p>
            </a>
            <ul>
                <li><a href="/OpenNMT-tf">Documentation</a></li>
                <li><a href="/Models-tf">Pretrained models</a></li>
            </ul>
        </div>
    </div>
</p>

Each implementation has its own set of [unique features](/features) but shares similar goals:

* Highly configurable model architectures and training procedures
* Efficient model serving capabilities for use in real world applications
* Extensions to allow other tasks such as text generation, tagging, summarization, image to text, and speech to text

**The OpenNMT ecosystem also includes projects to cover the full NMT workflow:**

<p>
    <div class="cards" id="cards-secondary">
        <div class="card">
            <a class="card-main" title="See on GitHub" href="https://github.com/OpenNMT/CTranslate2">
                <div class="project"><strong>CTranslate2</strong></div>
                <p>Efficient inference engine for Transformer models on CPU and GPU.</p>
            </a>
            <ul>
                <li><a href="/CTranslate2">Documentation</a></li>
            </ul>
        </div>
        <div class="card">
            <a class="card-main" title="See on GitHub" href="https://github.com/OpenNMT/Tokenizer">
                <div class="project"><strong>Tokenizer</strong></div>
                <p>Fast and customizable text tokenization library with BPE and SentencePiece support.</p>
            </a>
            <ul>
                <li><a href="https://github.com/OpenNMT/Tokenizer/blob/master/bindings/python/README.md">Documentation</a></li>
            </ul>
        </div>
    </div>
</p>
