---
layout: page
title: About
order: 5
---


OpenNMT was originally developed by <a href="http://yoon.io">Yoon Kim</a> and <a href="http://nlp.seas.harvard.edu" title="Natural language processing research group at Harvard SEAS">harvardnlp</a>.

<center>
<a href="http://nlp.seas.harvard.edu"><img style="margin: 50px auto;" width="200px" src="http://lstm.seas.harvard.edu/logo_nlp.png" alt="Natural language processing research group at Harvard SEAS" /></a>
</center>

Major source contributions and support come from <a href="http://www.systrangroup.com/" title="SYSTRAN - PURE NEURAL MACHINE TRANSLATION - ARTIFICIAL INTELLIGENCE AND DEEP LEARNING">SYSTRAN</a>.

<center>
<a href="http://www.systrangroup.com/"><img style="margin: 50px auto;" width="200px" src="/public/systran-logo-portrait.svg" alt="SYSTRAN - PURE NEURAL MACHINE TRANSLATION - ARTIFICIAL INTELLIGENCE AND DEEP LEARNING" /></a>
</center>

## Technical Report 

A <a href="https://arxiv.org/abs/1701.02810">technical report</a> on OpenNMT is available. If you use the system for academic work, please cite:

    @ARTICLE{2017opennmt,
             author = { {Klein}, G. and {Kim}, Y. and {Deng}, Y. 
                        and {Senellart}, J. and {Rush}, A.~M.},
             title = "{OpenNMT: Open-Source Toolkit 
                       for Neural Machine Translation}",
             journal = {ArXiv e-prints},
             eprint = {1701.02810} }

    
## Research

The main model is based on the papers:

* [Neural Machine Translation by Jointly Learning to Align and Translate](https://arxiv.org/abs/1409.0473) Bahdanau et al. ICLR 2015 
* [Effective Approaches to Attention-based Neural Machine Translation](http://stanford.edu/~lmthang/data/papers/emnlp15_attn.pdf), Luong et al. EMNLP 2015.


There are a lot of additional options on top of the baseline model. Specifically, there are functionalities which implement:

* [Effective Approaches to Attention-based Neural Machine Translation](http://stanford.edu/~lmthang/data/papers/emnlp15_attn.pdf). Luong et al., EMNLP 2015.
* [Character-based Neural Machine Translation](https://aclweb.org/anthology/P/P16/P16-2058.pdf). Costa-Jussa and Fonollosa, ACL 2016.
* [Compression of Neural Machine Translation Models via Pruning](https://arxiv.org/pdf/1606.09274.pdf). See et al., CoNLL 2016.
* [Sequence-Level Knowledge Distillation](https://arxiv.org/pdf/1606.07947.pdf). Kim and Rush., EMNLP 2016.
* [Deep Recurrent Models with Fast Forward Connections for Neural Machine Translation](https://arxiv.org/pdf/1606.04199).
Zhou et al, TACL 2016.
* [Guided Alignment Training for Topic-Aware Neural Machine Translation](https://arxiv.org/pdf/1607.01628). Chen et al., arXiv:1607.01628.
* [Linguistic Input Features Improve Neural Machine Translation](https://arxiv.org/pdf/1606.02892). Senrich et al., arXiv:1606.02892
* [Neural Machine Translation of Rare Words with Subword Units](https://www.aclweb.org/anthology/P/P16/P16-1162.pdf). Senrich et al., ACL 2016.


## Acknowledgments

Our implementation utilizes code from the following:

* [Andrej Karpathy's char-rnn repo](https://github.com/karpathy/char-rnn)
* [Wojciech Zaremba's lstm repo](https://github.com/wojzaremba/lstm)
* [Element rnn library](https://github.com/Element-Research/rnn)

## License

MIT

