# GAN-BERT (in Pytorch and compatible with HuggingFace)

This is an implementation in Pytorch (and **HuggingFace**) of the GAN-BERT method from https://github.com/crux82/ganbert which is available in Tensorflow.

While the original GAN-BERT was an extension of BERT, this implementation can be adapted to several architectures, ranging from Roberta to Albert!

**NOTE**: given that this implementation is different from the original one in Tensorflow, some results can be slighty different (but it alway improves the original BERT implementation).

## GANBERT

This is the code for the paper **"GAN-BERT: Generative Adversarial Learning for Robust Text Classification with a Bunch of Labeled Examples"** published at **ACL 2020 - short papers** by *Danilo Croce* (Tor Vergata, University of Rome), *Giuseppe Castellucci* (Amazon) and *Roberto Basili* (Tor Vergata, University of Rome).

GAN-BERT is an extension of BERT which uses a Generative Adversial setting to implement an effective semi-supervised learning schema. It allows training BERT with datasets composed of a limited amount of labeled examples and larger subsets of unlabeled material. 
GAN-BERT can be used in sequence classification tasks (also involings text pairs). 

This code runs the GAN-BERT experiment over the TREC dataset for the fine-grained Question Classification task. We provide in this package the code as well as the data for running an experiment by using 2% of the labeled material (109 examples) and 5343 unlabeled examples.
The test set is composed of 500 annotated examples.

As a result, BERT trained over 109 examples (in a classification task involving 50 classes) achieves an accuracy of ~13% while GAN-BERT achieves an accuracy of ~42%.

## The Model

GAN-BERT is an extension of the BERT model within the Generative Adversarial Network (GAN) framework (Goodfellow et al, 2014). In particular, the Semi-Supervised GAN (Salimans et al, 2016) is used to make the BERT fine-tuning robust in such training scenarios where obtaining annotated material is problematic. In fact, when fine-tuned with very few labeled examples the BERT model is not able to provide sufficient performances. With GAN-BERT we extend the fine-tuning stage by introducing a Discriminator-Generator setting, where:

- the Generator G is devoted to produce "fake" vector representations of sentences;
- the Discrimator D is a BERT-based classifier over k+1 categories.

![GAN-BERT model](https://github.com/crux82/ganbert/raw/master/ganbert.jpg)

D has the role of classifying an example with respect to the k categories of the task of interest, and it should recognize the examples that are generated by G (the k+1 category). 
G, instead, must produce representations as much similar as possible to the ones produced by the model for the "real" examples. G is penalized when D correctly classify an example as fake.

In this context, the model is trained on both labeled and unlabeled examples. The labeled examples contributes in the computation of the loss function with respect to the task k categories. The unlabeled examples contributes in the computation of the loss functions as they should not be incorrectly classified as beloning to k+1 category (i.e., the fake category).

The resulting model is demonstrated to learn text classification tasks starting from very few labeled examples (50-60 examples) and to outperform the classifcal BERT fine-tuned models by large margin in this setting.

More details are availale at: https://github.com/crux82/ganbert

## Citation

To cite the paper, please use the following:

```bibtex
@inproceedings{croce-etal-2020-gan,
    title = "{GAN}-{BERT}: Generative Adversarial Learning for Robust Text Classification with a Bunch of Labeled Examples",
    author = "Croce, Danilo  and
      Castellucci, Giuseppe  and
      Basili, Roberto",
    booktitle = "Proceedings of the 58th Annual Meeting of the Association for Computational Linguistics",
    month = jul,
    year = "2020",
    address = "Online",
    publisher = "Association for Computational Linguistics",
    url = "https://www.aclweb.org/anthology/2020.acl-main.191",
    pages = "2114--2119"
}
```

## Thanks 

We would like to thank ...