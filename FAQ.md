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

### How can I trust that the current version of OpenNMT is working?

We run a daily integration test of the system on EC2 to check that it is functioning
properly. The logs of the system are publicly available in the <a href="https://github.com/OpenNMT/IntegrationTesting/tree/master/logs">integration test</a> repo.  

## Models

### How can I replicate the full-scale NMT translation results? 

We have posted a complete <a href="http://forum.opennmt.net/t/training-english-german-wmt15-nmt-engine/29">tutorial</a> for training a German-to-English translation system on standard data. 


### Are there pretrained translation models that I can try?

There are several different pretrained models available on the <a href="http://opennmt.net//Models/">models</a> page. 

### Where can I get training data for translation from X-to-X?

Try the <a href="http://opus.lingfil.uu.se/">OPUS</a> Project. An open-source collection of parallel corpora. After stripping XML tags, you should be able to use the raw files directly in OpenNMT. 

### I am interested in other seq2seq-like problems such as summarization, dialogue, tree-generation. Can OpenNMT work for these?

Yes. OpenNMT is a general-purpose attention-based seq2seq system. There is very little code that is translation specific, and so it should be effective for many of these applications. 

For the case of summarization, OpenNMT has been shown to be more effective than neural systems like <a href="https://github.com/facebook/NAMAS">NAMAS</a>, and will be supported going forward. See the <a href="http://opennmt.net//Models/">models</a> page for a pretrained summarization system on the Gigaword dataset. 

### I am interested in variants of seq2seq such as image-to-sequence generation. Can OpenNMT work for these? 

Partially. OpenNMT can be extended with additional Torch neural networks, and a bit of coding. As an example, we have implemented a relatively general-purpose <a href="http://github.com/OpenNMT/im2text">im2text</a> system, with a small amount of additional code. Feel free to use this as a model for extending OpenNMT. 

## Additional Features

### Is the OpenNMT demo server available?

Unfortunately we cannot open-source the demo server. However, you can run OpenNMT in <a href="http://opennmt.net/OpenNMT/tools/servers/">server mode</a>. Contributions are welcome. 

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
