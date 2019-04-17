---
title: sentence boundary detection
keywords: scam mail, purify scam mail, sentence boundary detection
last_updated: October 14, 2017
tags: [소개, 프로젝트, 보안, 정제]
summary: "sentence boundary detection for non grammatical scam mails."
sidebar: project_sidebar
permalink: sentence-boundary-detection.html
folder: project
---

# Sentence boundary detection

## Purpose

Scam mails should be devided into sentence. Since most of them are non-grammatical, We need to purify and devide them. 

## puncatuate

### motivaiton

Some of scam mails missed thier many puncuates and spaces, so it was hard to detect sentence boundary. We used punctuator for increasing result. You can see this algorithm on this [paper](http://www.isca-speech.org/archive/Interspeech_2016/pdfs/1517.PDF) and code [here](https://github.com/ottokart/punctuator2).  

### idea

punctuator2 trained twice.  

1. ${bidirectional}^{\[2\]}{GRU}^{\[1\]}$ model with ${attention-mechanism}^{\[3\]}$, and ${late-fusion}^{\[4\]}$.
2. with late fusion output, add $pause-duration^{\[5,6\]}$ and adapt to target domain, the second stage discards the first stage output layer and replaces it with a new recurrent GRU layer.

Main is GRU-model(simillar with LSTM but simpler one). It has benefit for long sentences.  
**U**, **W** are weights, **t** is time, and $X = (x_1,x_2, .... , x_t)$ is one hot encoded words. tanh is used for non-linearity.

![GRU](https://zerobugplz.github.io/images/project/gru.png)  

- $$z = \sigma(x_tU^z + s_{t-1} W^z)$$  
- $$r = \sigma(x_t U^r +s_{t-1} W^r)$$  
- $$h = tanh(x_t U^h + (s_{t-1} \circ r) W^h)$$  
- $$s_t = (1 - z) \circ h + z \circ s_{t-1}$$  

It used not simple GRU model, but bidirectional-model with attention-mechanism.  
Input words are first processed by bidirectional layer consisting of two recurrent layers with GRU units, where one recurrent layer processes the sequence in forward direction and the other in reverse direction. Both of directions share weight.

### Method

![punctuator_algorithm](https://zerobugplz.github.io/images/project/punctuator.png)  

a is attention fuction.  
- $$\overrightarrow{h}_t = GRU({x_e}{W_t},[\overrightarrow{h}_{t-1},\overleftarrow{h}_{t-1}])$$  
- $$s_t = GRU(h_t, s_{t-1})$$  
- $$a_{ij} = \frac{exp(e_{ij})}{\sum_{k=1}^{T_x}{exp(e_{ik})}}$$  
- $$e_{ij} = a(s_{i-1},h_j)$$  

This layer processes the bidirectional states sequentially and keeps track of the current position in text, while the attention mechanism can focus on relevant bidirectional context aware word representations before and after the current position.  
<br />
$f_t$ is late fusion output : $f_t = {a_t}{W_{fa}}\circ\sigma({a_t}{W_{fa}}{W_{ff}}+{h_t}{W_{fh}}+b_f) + h_t$ is fed to the output layer producing the punctuation probabilities $y_t$ at time step t  
<br />
$$y_t = Softmax({f_t}{W_y}+b_y)$$  
<br />
This is first training. For two-stage training, to incorporate pause-duration and adapt to target domain, the second stage discards the first stage output layer and replaces it with a new recurrent GRU layer.  
  
$$z_t = GRU([f_t,p_t],z_{t-1})$$  

$f_t$ is late fusion output, $p_t$ is the pause duration before word $x_t$ as input.

### code in our system

Our code is on [github](https://github.com/zerobugplz/social-engineering-defense/tree/sentence_boundary_detection/sentence_boundary_detection/punctuator2-1.0). you should download [pre-training dataset](https://drive.google.com/drive/folders/0B7BsN5f2F1fZQnFsbzJ3TWxxMms) to run punctuator. Then just run [play_with_model.py](https://github.com/zerobugplz/social-engineering-defense/blob/sentence_boundary_detection/sentence_boundary_detection/punctuator2-1.0/play_with_model.py) with your text dataset. I use scam mail here, so I had already punctuation(but not accuracy).  
I punctuate only if there is no period or question mark nearby.  
Since some email was just empty and punctuator rid of them 

### Training details

- Adagrad optimizer : learning rate 0.02
- L2-norm < 2
- 5 epochs early termination
- weight : normalizer initialization
- hidden layer 256
- activation function : tanh
- mini-batches : 128
- trained by Theano framework
- data : [INTERSPEECH-T-BRNN-pre.pcl](https://drive.google.com/drive/folders/0B7BsN5f2F1fZQnFsbzJ3TWxxMms)

### reference

1. gated recurrent units (GRU) : K. Cho, B. Van Merrienboer, C. Gulcehre, D. Bahdanau, ¨F. Bougares, H. Schwenk, and Y. Bengio, “Learning phrase representations using rnn encoder-decoder for statistical machine translation,” arXiv preprint arXiv:1406.1078, 2014.
2. Bidirectional recurrent neural networks : M. Schuster and K. K. Paliwal, “Bidirectional recurrent neural networks,” IEEE Transactions on Signal Processing, vol. 45, no. 11, pp. 2673–2681, 1997.
3. Neural machine translation by jointly learning to align and translate
4. late fusion approach : T. Wang and K. Cho, “Larger-context language modelling,” arXiv preprint arXiv:1511.03729, 2015.
5. pause feature1 : H. Christensen, Y. Gotoh, and S. Renals, “Punctuation annotation using statistical prosody models,” in ISCA Tutorial and Research Workshop (ITRW) on Prosody in Speech Recognition and Understanding, 2001.
6. pause feature2 : J. Kolar, J. Svec, and J. Psutka, “Automatic punctuation annotation in Czech broadcast news speech,” in SPECOM 2004, Saint Petersburg, Russia, 2004.

### mentioned part in our paper

Some of scam mails missed their punctuations. Most of "detecting sentence boundary algorithms" perform better with appropriate punctuation. We use ${Punctuator}^{[1]}$ : bidirectional recurrent neural network model with attention mechanism. It can be trained twice with text file and audio file. Text file should have clear period, comma, and question mark. Audio file should be re-writed to text file with silence time. If silence time is long, it judges as independent senteces and put period. If it is just a little time, put comma. If it doesn't have silence time, put nothing. Punctuator was trained with Europarl v7 monolingual English corpus(text file), and IWSLT 2012 TED task(audio file) for 256 hidden layer, 0.02 learning rate, and 5 epochs. Trained punctuator's input is text-file and output is punctuated text file(commas, periods, question marks, exclamation marks, colons, semicolons and dashes). You can see more detail at annotation \[1\].  

1. Bidirectional Recurrent Neural Network with Attention Mechanism : Ottokar Tilk, Tanel Alumae, "Bidirectional Recurrent Neural Network with Attention Mechanism for Punctuation Restoration" INTERSPEECH 2016 September 8–12, 2016. San Francisco, USA

## sentence tokenize with Punkt.

### motivation

It is one of the most popular sentence tokenizer algorithm in the world. It performs well and easy to use. 

### structure

![punkt_structure](https://zerobugplz.github.io/images/project/punkt_structure.png)  

- <S> Sentence Boundary
- <A> Abbreviation
- <E> Ellipsis
- <A><S> Abbreviation at the End of Sentence <E><S> Ellipsis at the End of Sentence

### code in our system

Punkt algorithm has dependency with space between sentence and sentece because if sentences are not separated by spaces but with period, the algorithm detects it as a abbreviation in many cases. So I make a space when period is not used for abbreviation('Mr.', 'Ms.', 'Mrs.', 'www.', '@', 'Dr.', 'mr.', 'mrs.', 'dr.', 'Www.', 'http', 'Co.', and 'co.').

### mentioned part in our paper

To parse text by sentence, we segmented the scam mails into sentences using the punkt algorithm. ${Punkt}^{[1]}$ is based on the assumption that a large number of ambiguities in the determination of sentence boundaries can be eliminated once abbreviations have been identiﬁed. It uses an unsupervised algorithm to build a model for abbreviation words, collocations, and words that start sentences. You can see more detail at annotation [1]. The punkt algorithm works well in most cases, but in the case of a sentence that has not been properly spaced, it has not recognized it as a sentence, but has recognized it as an internal point. So we added spacing by searching for lowercase capitalized words except for (Mr., Mrs., Ms., Dr., www., Co.) and then after, we used punkt algorithm.

1. Sentence Boundary Detection :  Tibor Kiss and Jan Strunk, "Unsupervised Multilingual Sentence Boundary Detection", 2006 Massachusetts Institute of Technology