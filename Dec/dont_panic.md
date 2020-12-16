# Don’t Panic! Better, Fewer, Syntax Errors for LR Parsers

## Motivation to Read
我手头的一个项目是关于评估Java的语法错误自动修复工具的。我们可以将Java分成两类，一类是使用机器学习的方法，如RLAssit和Deepfix等；另一类则是传统的LR-Parse error recovery方法。这一篇暂时应该是LR-Parser中最出色的一篇。

我本身并没有PL的背景，因此针对这篇文章并没法说太多，以及在此基础上进行实质性的改进。

## 如何使用此工具
作者将文章的代码[开源](https://github.com/softdevteam/grmtools)了，但是有一说一我并不懂Rust，因此我之前想改代码并没有成功。问了作者，作者还提供了可以直接使用的[工具](https://github.com/softdevteam/grmtools/tree/master/nimbleparse)。

但是它给出的结果并不是“程序代码”，而是一个compilation_unit，所以我自己写了程序 [token_to_source()](https://github.com/yangzhou6666/SyntaxRePro/blob/master/CPCT%2B/parser_experiment.py) 将compilation unit reverse回Java程序，然后使用javac-parser来检测修复后的代码有哪些语法错误。