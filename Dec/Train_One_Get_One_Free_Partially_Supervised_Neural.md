# Train One Get One Free: Partially Supervised Neural Network for Bug Report Duplicate Detection and Clustering

Venue: NAACL
年份: 2019

同样的，这篇也是关于duplicate bug report detection的，不过这篇是发在NLP领域的，应该是SE还是有一些区别。又是老paper重读，每次都有新体验。

这篇文章提出了一个neural architecture，来联合dectect if two bug reports are duplicates, and aggregate them into latent topics

这篇文章是考虑了duplicate classification

### motivation

developing a framework that can automatically identify duplicate bug reports and cluster them without requiring additional labels

亮点：提出了一个假设: **determining the feature discussed in a report** is a sub-task of detecting whether or not a report is a duplicate to another one

也就是说要找到一个report里提到的features是什么

这个工作是用了Siamese architectures for modeling pairs of texts, they use a shared Recurrent Neural Network (RNN) to encode the two reports

two-step attention module

1. learn a self-attention for topic similarity modeling
2. learn a conditional attention using a memory vector for duplicate classification

### Contributions

1. They propose a neural model for multi-task learning that requires supervision for only one of the tasks
2. semantic space decomposition and a hierarchical-conditional attention module to perform the tasks of duplicate detection and topic based clustering

## Proposed Method

Given a pair of reports P and Q, the system uses a single binary label $r(P,Q)$ to supervise both tasks

duplicate classification, topic similarity modeling

### Text Encoder

把一个bug report作为a sequence of words ${w_1, w_2, ..., w_n}$ as input, 然后encode它变成 latent vectors $h_1, h_2,...,h_n$

bi-directional GRU units to encode the context information around a word

### Semantic Space Decomposition

we force the network to learn topical information about each word in the ﬁrst k dimensions of its latent vector space

### Topic Similarity Modeling

We aggregate the topic vectors of the constituent words to represent the topic of a report, and use a self-attention layer to learn the weights of the words important in determining the topic.

we normalize the loss using proportional class weights

### Duplicate Classification

they use another attention layer for this component to allow the network to focus on important words

## Evaluation

### Evaluation Duplicate Classification

**Baselines**

1. Logistic Regression
2. Siamese CNN
3. Siamese Bi-GRU
4. Siamese Bi-GRU with Attention
5. DWEN
6. BiMPM

### Evaluating Clusters

baseline是LDA

这篇文章的亮点是，不仅分类了是否是duplicate，还cluster them into meaningful latent topics without additional supervision