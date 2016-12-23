---
layout: page
title: FAQ
order: 4
---

* TOC
{:toc}


## General

### Why neural machine translation (NMT)?

We care about neural machine translation for several reasons.

1) Results show that NMT produces automatic translations that are
significantly preferred by humans to other machine translation
outputs. This has led several companies to switch NMT-based
translation systems.

2) Similar methods (often called seq2seq) are also effective for many
other NLP and language-related applications such as dialogue, image
captioning, and summarization. A recent talk from HarvardNLP describing some of these recent
advances is available <a
href="https://harvardnlp.github.io/seq2seq-talk/slidescmu.pdf">here</a>.

3) NMT has been used as a representative application of the recent
success of deep learning-based artificial intelligence. For instance a
recent <a href="http://www.nytimes.com/2016/12/14/magazine/the-great-ai-awakening.html">NYT
magazine cover story</a> focused on Google's NMT system.


### Where can I go to learn about NMT? 

We recommend starting with the ACL'16 NMT <a
href="https://sites.google.com/site/acl16nmt/home">tutorial</a>
produced by researchers at Stanford and NYU. The tutorial also
includes a detailed bibliography describing work in the field.

### What do I need to train an NMT model?

You just need two files: a source file and a target file. Each with
one sentence per line with words space separated. These files can come from
standard free translation corpora such a WMT, or it can be any other sources
you want to train from.


## Installation / Setup

### What type of computer do I need to train with?

While in theory you can train on any machine; in practice for all but
trivally small data sets you will need a GPU that supports CUDA if you
want training to finish in a reasonable amount of time. For
medium-size models you will need at least 4GB; for full-size
state-of-the-art models 8-12GB is recommend.

### How can I install this system on my own system (with or without root)?

Follow the quick-start instructions on the <a href="http://torch.ch/docs/getting-started.html">Torch page</a>.


### How can I use this system with Docker (on Ubuntu)?

First you need to install `nvidia-docker`.

```wget -P /tmp https://github.com/NVIDIA/nvidia-docker/releases/download/v1.0.0-rc.3/nvidia-docker_1.0.0.rc.3-1_amd64.deb
sudo dpkg -i /tmp/nvidia-docker*.deb```

If this command does not work, you may need to run the following updates, 

```sudo apt-add-repository 'deb https://apt.dockerproject.org/repo ubuntu-xenial main'
sudo apt-get update
sudo apt-get install docker-engine nvidia-modprobe```

Then simply run our Docker container

```sudo nvidia-docker run -it harvardnlp/opennmt:8.0 .```

Once in the instance, check out the latest code

```git clone https://github.com/opennmt/opennmt.git```

### How can I use this system on Amazon/Google cloud?

The best way to do this is through Docker. We have a public AMI with the preliminary
CUDA drivers installed: `ami-c12f86a1`. Start a P2/G2 GPU instance with this AMI and
run the `nvidia-docker` command above to get started. 

### How can I use OpenNMT as a library?

You can install OpenNMT as a library in the standard way,

```luarocks make rocks/opennmt-scm-1.rockspec```

## Contributions

### Can I send a pull request?

That would be great. Just be sure to read the `STYLE.md` before you submit. 

### Where do the developers talk?

We are normally in our <a href="https://gitter.im/OpenNMT/openmt">Gitter channel</a>. If you want to contribute come chat. We are friendly.

### Feature X would make OpenNMT even better!

That's not really a question, but we would love to add that feature! The quickest way to get it into OpenNMT
is to send us a pull request on GitHub. Just fork the repo, make the change, and click send pull request.

### But I don't know how to code...

Okay, that's fine, we can help implement it. Go to our <a href="http://forum.opennmt.net/">forum</a> and add a feature request. We will get to it soon.