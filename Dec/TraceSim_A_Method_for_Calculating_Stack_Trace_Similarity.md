# TraceSim: A Method for Calculating Stack Trace Similarity

## Motivation To Read
和组里的一个PhD Candiate在合作做关于Duplicte Bug Report Detection的内容，Bug Report中可能含有Stack Trace，因此这篇文章可能会有帮助。此外，也许这篇论文也会对Stack Trace-based Bug Localization会有一些灵感。

## 需要解决的问题
> Writing bug reports may require substantial effort from users. Therefore, in order to reduce this effort, a way to create such reports automatically is implemented in most widely used products. In most cases, information available at the time of crah, i.e. stack trace, is used to form a report.

写Bug Report费时费力，因此人们希望能够有自动生成Bug Report的方法。但这样的方法有缺陷：
> The draw back of this approach is the huge number of generated reports, the majority of which are duplicates (it is well-known that the same bug can produce slightly different reports). For example, in 2016 Firefox was receiving 2.2 million crash reports a day.

有一说一，我的确没想过有这样的缺陷。那讲道理其他的自动化生成方法是否有类似的缺陷呢？

关于automatically created bug reports，有两个流行的任务：
1. 给定一个report，找到与之相似的report并且按照相似度排序（ranked report retrieval）
2. 给定一组report，将他们分到不同的buckets中(report clusterization)


## Approach
在这篇论文中，作者通过计算两条stack trace之间的相似度来解决这个问题。Decuplication研究可以分成两块：基于TF-IDF或者基于Stack trace structure.
前者使用information retrieval approach，后者使用string matching algorithm(比如计算edit distance).但是就作者所知，现在还没有研究将这两种方法组合起来使用。

> Such combination may result in a superior quality of bucketing and may significantly outperform any method that belongs to these individual groups. To substantiate importance of this idea, we would like to quote Campbell et al. [5]: “a technique based on TF-IDF that also incorporates information about the order of frames on the stack would likely outperform many of the presented methods...”.

与此同时，机器学习也很少被应用到这个领域：当前大部分的相似度计算方法都不依赖机器学习技术。原因是传统方法比机器学习方法更加的鲁邦和稳定，这一点对于此任务非常重要。因此，作者的想法是将传统方法作为基础，并结合机器学习技术来设计更好的similarity function。

总结来说，这篇文章的贡献是TraceSim:
> the first algorithm for computing stack trace similarity that structurally combines TF-IDF [25] and string distance while using machine learning to improve quality.

### 如何纳入机器学习方法？
作者说，文章的想法是将传统方法作为基础，并结合机器学习技术来设计更好的similarity function，究竟是什么意思呢？
作者还是用一些传统的方法定义了相似度，比如Frame Weight Computation, Levenshtein Distance Calculation。但是这些计算公式中有一些超参数。作者`Estimate hyperparameter via machine learning`.
> To obtain their values (hyperparameters) we formulate an optimization problem and approach it with machine learning. The idea is to optimize the ROC AUC [10] metric by training on a manually labelled part of the stack trace dataset.

## Dataset
这是篇企业论文，论文使用的数据并没有公开。数据来自于Jetbrain内部。


## Results
我并没有很细致地去看效果如何，作者提到：
> The evaluation on a manually labeled dataset shows significantly better results compared to baseline approaches.

并且这个系统已经在Jetbrain内部使用了。

## Summary
总体而言并没有很强的创新性，作为一片Workshop论文是OK的。不过将传统方法作为基础，使用Machine learning来进行搜索的思路没准也可以做。

