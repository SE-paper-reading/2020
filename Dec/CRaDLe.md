# CRaDLe: Deep Code Retrieval Based on Semantic Dependency Learning

### Tags

Code retrieval; semantic dependency; dependency learning; neural network

code retrieval aims at searching the most relevant ones from a set of code snippet

难点：mitigating the semantic gap between natural language descriptions and code snippets

With the ever-increasing amount of available open-source code, recent studies resort to neural networks to learn the semantic matching relationships between the two sources

作者提出了a novel approach for Code Retrieval based on statement-level semantic Dependency Learning.  Speciﬁcally, CRaDLe distills code representations through fusing both the dependency and semantic information at the statement level, and then learns a uniﬁed vector representation for each code and description pair for modeling the matching relationship

utilize statement-level dependency relations in a code snippet based on Program Dependency Graph (PDG).

CRaDLe is the ﬁrst code retrieval approach that integrates the dependency and semantics information at the statement level for learning code representations.

### Architecture

<code, description> pairs

separately encoded into vectors by the code encoder and query encoder respectively