# Statistical Machine Translation Outperforms Neural Machine Translation in Software Engineering: Why and How

## Motivation to read
之前做Syntax error repair的时候，有很多工作是用nueral machine translation做的，这篇文章说statistical machine translation效果更好，那也许可以换些方法？我们在做Bug Localization和duplication bug report detection，现在也是想尝试BERT(隶属于neural machine translation)，但是效果并不好。也许这篇文章可以给一点原因。

## Summary

a hypothesis that SE corpus has inherent characteristics that NMT will confront challenges compared to the state-of-the-art translation engine based on Statistical Machine Translation.

Prefix Mapping:
> We introduce a problem which is significant in SE and has characteristics that challenges the ability of NMT to learn correct sequences, called Prefix Mapping.

Results
> By the evaluation, we show that SMT outperforms NMT for this research problem, which provides potential directions to optimize the current NMT engines for specific classes of parallel corpus.

这里的parallel corpus是啥嘛

## Concepts
* NMT和SMT的区别是什么？
* 解释一下Prefix Mapping这个任务
* 三种文档：Natural Language, Software Documentation, Programming Language；使用这三种文档作为输入的主要有哪些任务？
* NMT用于SE任务上的优缺点
* SMT用于SE任务上的优缺点呢？
* 什么是unknow words problems in translation engine



## 一些想法

用NMT这某种成都上也算“语法上的类比”？
