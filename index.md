---
layout: index
title: Home
order: 1
---

**OpenNMT** is an open source ecosystem for neural machine translation and neural sequence learning.

<center><img width="80%" src="/simple-attn.png" /></center>

Started in December 2016 by the [Harvard NLP](https://nlp.seas.harvard.edu/) group and SYSTRAN, the project has since been used in [several research and industry applications](/publications). It is currently maintained by [SYSTRAN](http://www.systransoft.com/) and [Ubiqus](https://www.ubiqus.com/).

**OpenNMT provides implementations in 2 popular deep learning frameworks:**

<p>
    <div class="cards" id="cards-primary">
        <div class="card">
            <a class="card-main" title="GitHub" href="https://github.com/OpenNMT/OpenNMT-py">
                <img src="public/pytorch.png" alt="PyTorch"/>
                <div class="project"><strong>OpenNMT-py</strong></div>
                <p>User-friendly and multimodal implementation benefiting from PyTorch ease of use.</p>
            </a>
            <ul>
                <li><a href="http://opennmt.net/OpenNMT-py">Documentation</a></li>
                <li><a href="/Models-py">Pretrained models</a></li>
            </ul>
        </div>
        <div class="card">
            <a class="card-main" title="GitHub" href="https://github.com/OpenNMT/OpenNMT-tf">
                <img src="public/tensorflow.png" alt="TensorFlow"/>
                <div class="project"><strong>OpenNMT-tf</strong></div>
                <p>Modular and stable implementation relying on the TensorFlow ecosystem.</p>
            </a>
            <ul>
                <li><a href="http://opennmt.net/OpenNMT-tf">Documentation</a></li>
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
            <a class="card-main" title="GitHub" href="https://github.com/OpenNMT/Tokenizer">
                <div class="project"><strong>Tokenizer</strong></div>
                <p>Advanced tokenization library with C++ and Python APIs.</p>
            </a>
        </div>
        <div class="card">
            <a class="card-main" title="GitHub" href="https://github.com/OpenNMT/nmt-wizard-docker">
                <div class="project"><strong>nmt-wizard-docker</strong></div>
                <p>Docker-based wrapper for training and translating using a standardized interface.</p>
            </a>
        </div>
        <div class="card">
            <a class="card-main" title="GitHub" href="https://github.com/OpenNMT/nmt-wizard">
                <div class="project"><strong>nmt-wizard</strong></div>
                <p>Tasks launcher and monitor on remote platforms (SSH, EC2, etc.).</p>
            </a>
        </div>
    </div>
</p>
