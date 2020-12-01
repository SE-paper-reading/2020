# Code Recommendation for Exception Handling
非常不错的论文，今天粗看了一下，值得再看认真研读，虽然问题不同，但是可以从中找到很多和自己研究相关的内容!

## Motivation to Read
之前跟David讨论关于AI System中的Control Flow时，他忽然想到了一篇文章，说程序员经常在Error Handling部分犯错，或者写的很简略。刚好今年的FSE发了这样一篇文章，就顺手看了下。如果有用的话自己之后也可以使用。

## Some idea
- 不从代码中获得数据，而是从互联网中获得数据，比如Stackoverflow上某些API和特定类型的Exception经常出现；
- 能否和Static Analysis结合，在自己写代码的时候，可以出现这样的情况“定义了一个函数，函数中调用了某个API，然后调用自己自定义的函数”，也许可以用静态分析的方法找到这段code snip中的所有API，然后再分析。或者用这样的思路，再去做本文中的数据处理。可能会有不一样的结果。

## 不熟悉的概念

`fuzzy logic`

## Summary

这篇论文介绍了FuzzyCatch：a recommendation tool for handling exceptions. 给定一段代码片段，这个工具能够基于Fuzzy Logic预测是否会发生运行时异常，并能够推荐处理此异常的代码。FuzzyCatch已经被做成了一个Android Studio的插件。

据作者说效果很好，在预测哪个exception会发生时，有77%的top1准确率；在推荐当异常发生时什么方法应该被调用上，也有70%的准确率。

## Background

- Exception Handling很重要，用如下来佐证：

> Exceptions are unexpected errors occurring while a program is running. If not handled properly, exceptions could lead to serious problems such as system crashes or resource leaks. For example, when a program tries to parse an integer from a string but the string does not represent a valid number, a NumberFormatExcep- tion exception occurs. If the program ignores that exception and continues to read, it will crash. Thus, effective exception handling is important in software development. A prior study [38] reports that correctly handling exceptions could improve 17% in the per- formance of software systems.

- Learning to handle exceptions很难，主要是因为：

> First, modern software development relies strongly on API libraries. An API library often defines many specific exception types and exception handling rules. However, a major API library often consists of a large number of components. For example, the Android application framework contains over 3,400 classes, 35,000 methods, and more than 260 exception types [22]. Thus, it is very difficult to learn and memorize what method could cause what exception and what to react when a particular exception occurs. Secondly, popular API libraries are often upgraded quickly. Most importantly, the documentation for exception handling is generally insufficient.

概括一下：

1. 当代软件开发主要依赖API libraries，而这些libraries经常会定义很多特殊的exception类型。
2. 这些API libraries更新迭代非常快
3. 关于exception handling的文档总体来说不够

- 另一个业界缺陷：当前的IDE没有办法给用户提供关于exception handling的好建议

- 基本思路：

将exception handling看为两个问题：

1. 调用函数m然后捕获异常e
2. 如果异常发生，采取行动对其做出反应

FuzzyCatch通过大量的高质量代码学到了exception handling的规则。假设没有文档告诉我们，当调用m时，我们需要捕捉异常。但是如果从成千上万的安卓应用中我们也许能够发现这样的规则。但是因为这样的规则通常不完美，所以使用fuzzy logic来表示和组合他们。

## 数据集

### 训练集合

> We collected a dataset containing over 21 million methods from over 13,000 highly rated mobile apps in Google Android Appstore.

> We collected a second dataset of 1,000 real exception related bugs. In its strictest mode, FuzzyCatch flags 734 cases (73%), i.e., suggesting they need exception handling. In its loosest mode, Fuzzy- Catch flags 821 cases (82%).

这里两种模式的区别应该也就是我们说的trustworthy.

> The source code of most Android apps is not publicly available. With few apps with source code available, training FuzzyCatch from existing mobile app projects would be difficult and insuffi- cient. Thus, we decided to train our models with Android bytecode.

牛逼，怎么在bytecode上训练呢？

> Next, we developed a bytecode analyzer that analyzed each class and looked for all methods in the class to build GROUM models

原来是自己做了一个

> In the end, we analyzed over 26 million unique methods which have in total nearly 740 million bytecode instructions. They are used to train XRank and XHand, producing fuzzy logic rules for 261 exception types and 64,685 methods in Java and Android APIs.

### 测试集

> We first collected a dataset consists of several large open-source Android projects. For each project, we checked out its source code repository to retrieve all the code and commits. We developed an extraction tool to identify the bug fixes from the commits and issues of those projects.

> Next, we manually inspected all the bug fixes to identify exception bug fixes.

> Finally, we were able to collect a dataset of 1,000 exception bug fixes.

> The steps to identify the exception bug fixes and collect the dataset are described in detail in [31]. Figure 9 shows an exception bug fix in our dataset. The dataset is available at [rebrand.ly/ExDataset](http://rebrand.ly/ExDataset).

关于这一块数据收集的论文：An Empirical Study of Exception Handling Bugs and Fixes


## Approach

> Our key idea to solve this problem is to learn from the exception handling code already written in high-quality software systems.

基本思路就是，如果在这些代码中发现，大量调用某方法m的代码，都使用catch语句来捕获异常e，则说明调用m可能会产生e。在论文中，举了几个30%多的例子。

比例并不算很高，因此学到的规则imperfect，因此作者使用模糊逻辑来解决这个问题。

> In traditional fuzzy logic systems, membership functions are de- fined by domain experts. However, in FuzzyCatch, we define mem- bership functions empirically, i.e., the membership scores 𝜇𝑚 (𝑒) is estimated from the training data (a repository of high-quality code).

类似的话可以用在我们的Trustworthy的论文中，我们有办法采用类似的做法吗？
