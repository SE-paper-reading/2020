# Explainable AI for Software Engineering

今天读一篇水文，因为一直不太了解什么是AI4SE, SE4AI。这不刚好看到一篇文章吗，来读读。

such AI/ML models for software engineering are still impractical, not explainable, and not actionable

actionable? 

> AI4SE (or Software Analytics) is a sub-ﬁeld in software engineering that focuses on leveraging AI/ML and data analytics techniques to uncover interesting and actionable knowledge from the unprecedented amount of software data.

说道现在很多公司用AI/ML techniques来make data-driven engineering decisions，比如说有这么一些问题

- software defect prediction
- effort estimation
- task prioritization
- task recommendation
- expert recommendation
- code generation
- developers’ productivity prediction
- malware detection
- security vulnerability detection

prediction的问题比较多

## Case Study

### Problem

EXPLAINABLE DEFECT PREDICTION MODELS

an explainable defect prediction framework

- Generating ﬁne-grained predictions in order to help developers localize which lines of code are the most risky so developers can allocate limited software quality assurance activities in a cost-effective manner.
- Generating explanations for each prediction to help developers understand why a ﬁle is predicted as defective.
- Generating actionable guidance to help managers chart appropriate quality improvement plans.

They used LIME’s model-agnostic technique to explain the predictions of file-level defect prediction models.

然后就从三个角度：

- Help developers localize which lines of code are the most risky
- Help developers understand why a ﬁle is predicted as defective
- Help managers develop software quality improvement plans

## 结论

Explainable AI techniques can be brought into software engineering to provide explanations of the predictions and actionable guidance to support software engineering tasks

## Thoughts

此文太短，看完没啥感觉。下次还是要选一些比较技术一些的文章看看嗷（今天划水）