# DRAST - A Deep Learning and AST Based Approach for Bug Localization

# Motivation
multi-language bug localization

## Task
Bug Localization, an automated process for finding the list of probable buggy files in a project related to a given bug report.

## Related Work
- IR: bug report is taken as a query and outputs a list of documents (source files). IR-based bug localization approaches treat the textual information present in the bug report as a query and source code as a natural text and output the ranked list of source code files based on the textual similarity between the bug report and source files.

classs / method names, version history, similar bug histories, strutural information such as stack traces and segmentation

- ML/DL: reduce the 'lexical and semantic gap' between bug reports and source code, map the latent features present in the bug reports to source files

## State-of-the-art
- BugLocator
- DNNLOC
- DeepLocator
- NPCNN
- CAST

# Method
DRAST approach represents source code as code vectors by using its high-level AST and combines rVSM, an IR techinique with ML/DL models to rank the list of buggy files.

They also proposed *src2vec*, to generate code vectors from source code files such that each vector represents the block of the source code by using high-level AST representation of code.

## Code Blocks Generation
1. used srcML to generate program vectors from source code
2. parse the created XML file to convert the source code file into codeblocks/vectors
3. extracting code characteristics from source code file

## Feature Generation
1. input pre-processing

2. feature extraction
The pre-processed bug reports and code features are converted into tf-idf vectors.

3. Creating positive and negative pairs
- positive pairs: pairing bug reports with their corresponding buggy files
- negative pairs: pairing bug reports with the rest of the source code files

4. autoencoding
use autoencoder to reduce the dimensions

5. Feeding to DNN relevancy estimator

# Evaluation
## Accuracy@k
success or miss, accuracy@k will be considered as a ratio of success to the total number of bug reports

## Mean Average Precision (MAP)
a mean of average presicion values calculated for all predictions corresponding to each bug report

## Mean Reciprocal Rank (MRR)
a mean of reciprocal of the rank of the actual buggy file in the list of files predicted by the model

# Some thinkings
1. They represent the bug reports and code features as tf-idf vectors. Are tf-idf vectors better than word2vec? Maybe we can try tf-idf as well.

2. The model design has learned from DNNLoc. We can also get some inspiration from this model.

3. Should get some general ideas from the aforementioned models/architectures.