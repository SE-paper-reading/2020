# A First Look at the Integration of Machine Learning Models in Complex Autonomous Driving Systems


## Motivation: Why I read this paper?
Currently, I am working on analyzing trustworthy AI systems with static analysis. In recent years, the research community has made significant breakthroughs in machine learning algorithms and practical application. But little work has been done on analysing the AI-powered system. I don't want to target at AI models (single module in a system) only. Instead, I want to proceed with this project from a systematic perspective. 

This paper takes a first look at the integration of machine learning models in the autonomous driving system, which is helpful for me to understand my project, e.g. the feasibility to analyzing a large-scale autonomous driving system.

## Metadata
Zi Peng, Jinqiu Yang, Tse-Hsun (Peter) Chen, and Lei Ma. 2020. A first look at the integration of machine learning models in complex autonomous driving systems: a case study on Apollo. In Proceedings of the 28th ACM Joint Meeting on European Software Engineering Conference and Symposium on the Foundations of Software Engineering (ESEC/FSE 2020). Association for Computing Machinery, New York, NY, USA, 1240–1250. DOI:https://doi.org/10.1145/3368089.3417063

## Insights and Ideas

> Despite extensive study on ML models, it still lacks a comprehensive empirical study towards understanding the ML model roles, peculiar architecture and complexity of ADS.

> We present our findings on how the ML models interact with each other, and how the ML models are integrated with code logic to form a complex system.

Well, at least it proves that the Apollo system can be analyzed by several researchers.

> lack of adequate tests in general

Although automated driving system is safety-critical, it still lacks of adequate tests in general. Lack of manpower may explain the problem, but can the system be "no-easy-to-test"? Put a new word here -- testability which represents the difficulty to test a software system. Maybe the testability is low and how can we improve it? I don't know whether there are similar concepts in software engineering communities.



## Organize Research Questions