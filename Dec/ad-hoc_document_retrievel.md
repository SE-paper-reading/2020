# 概况
EMNLP 2020的论文，因为我们最近不是想要用BERT在信息检索吗，所以需要看一些目前在文档检索方面的工作

# 方法
a novel weaklysupervised method for training DL methods for ad-hoc document retrieval

受FAQs检索的启发，并假定文档有如下three fields:
- title
- abstract
- content

虽然这里说到三个域，但其实，content只是作为abstract来用的。就是当datasets have only title and content，他们会create the abstract by taking the first 512 tokens of the content。


## 假设
title是question，abstract是answer

the title and abstract fields are further used as a weaksupervision data source for training two independent BERT models

## first model
matches user queries to documents’ abstracts

## second model
matches user queries to titles

## 过程
the initial candidate documents retrieval uses pure IR similarities and relevance models

The re-ranking step exploits two independent weakly-supervised BERT models

The final re-ranking is obtained by combining the outcome of the baseline IR method and the two BERT-based re-rankers using an unsupervised late-fusion step.

# highlight
Our work is different from all those works as we train a model to generate title paraphrases that are used to enable query-to-title (question) matching and not only query-to-abstract (answer) matching.

we consider the adhoc document retrieval problem as an instance of FAQ retrieval, where a document’s title represents the question and its abstract the answer

## Enhanced ad-hoc retrieval using Fusion
Two-Step PoolRank (denoted TSPR) unsupervised fusion method – an extended PoolRank method that estimates document relevance using the three ranked lists (obtained by IR-Base, BERT-Q-a and BERTQ-t) as pseudo-relevance evidence sources.


# 想法
1. As a future work, we plan to utilize automatic summarization for missing abstracts, instead of taking the first 512 content tokens. 这篇文章也是只选了前512个tokens，看来这个是传统。也许我们也可以尝试用automatic summarization，对比一下，只选前512，比较效果。

2. 他们用了GPT-2来生成标题的paraphrases. 为什么要paraphrases?
文章里提到：Here our assumption is that by generating title paraphrases, we can train a model to match user queries to titles.

3. 不如也试试TSPR? 看上去很新颖。mark一下，明天看看 Haggai Roitman. 2018. Utilizing pseudo-relevance feedback in fusion-based retrieval. In Proceedings of the 2018 ACM SIGIR International Conference on Theory of Information Retrieval, ICTIR ’18, pages 203–206, New York, NY, USA. ACM.

4. 一个BERT不行，我们可以用两个。思路要开阔
