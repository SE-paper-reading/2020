这篇文章之前读过，但是读得不细致。现在要准备拓展，必然要读得细致一点。

# 问题

这个文章主要是针对BERT在一个句子集合里，找最相似的一对pair时需要很多时间这个问题，提出解决方案。

由于我们的问题实际上是document retrieval，那么sentence BERT或许不合适，但是这个训练方法我们可以借鉴。

## Drawbacks of BERT

看看BERT是如何操作的？

cross-encoder, 把两句话都pass到transformer network，然后预测目标值

no independent sentence embeddings are computed, which makes it difficult to derive sentence embeddings from BERT

### 以往的工作是如何得到sentence embeddings

Each sentence is prepended with a special [CLS] token, and we use the top-most hidden state corresponding to [CLS] as a vector representation of the whole sequence, as per the original work. 这就说明了对于一个bug report，我们也可以通过这种方式得到vector representation

# SBERT

SBERT fine-tunes BERT in a siamese / triplet network architecture.

fixed-sized vectors

use the pre-trained BERT and RoBERTa network and only fine-tune it to yield useful sentence embeddings

SBERT adds a pooling operation to the output of BERT or RoBERTa to derive a fixed sized sentence embedding. three pooling strategies:

1. using the output of CLS-token
2. computing the mean of all output vectors
3. computing a max-over-time of the output vectors (MAX-strategy)

objective functions:

1. classification objective function
2. regression objective function
3. triplet objective function

## Training Details

- 3-way softmax-classifier objective function for one epoch
- batch size 16
- Adam optimizer with learning rate 2e-5
- a linear learning rate warm-up over 10% of the training data

## Evalution

### Semantic Textual Similarity (STS)

- **Unsupervised STS**

siamese network structure and fine-tuning mechanism substantially improves the correlation

- **Supervised STS**

SBERT uses cosine-similarity to compare the similarity between two sentence embeddings.

We use the training set to fine-tune SBERT using the regression objective function. At prediction time, we compute the cosine-similarity between the sentence embeddings.

# Thoughts

SBERT看上去很简单。。也确实，相对于BERT，创新不太多，主要还是fine-tuning. 不过作者们开源了，所以让我们调用这些包比较方便。可以基于SBERT的框架做一些改动。