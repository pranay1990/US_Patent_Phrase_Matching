# U.S. Patent Phrase to Phrase Matching
To extract meaning from a large, text-based dataset derived from inventions.

# Project Motivation
In this competition, we had to train your models on a novel semantic similarity dataset to extract relevant information by matching key phrases in patent documents. Determining the semantic similarity between phrases is critically important during the patent search and examination process to determine if an invention has been described before. For example, if one invention claims "television set" and a prior publication describes "TV set", a model would ideally recognize these are the same and assist a patent attorney or examiner in retrieving relevant documents.

# Description about the data
In this dataset, we are given pairs of phrases (an anchor and a target phrase) and asked to rate how similar they are on a scale from 0 (not at all similar) to 1 (identical in meaning). This challenge differs from a standard semantic similarity task in that similarity has been scored here within a patent's context, specifically its CPC classification (version 2021.05), which indicates the subject to which the patent relates. For example, while the phrases "bird" and "Cape Cod" may have low semantic similarity in normal language, the likeness of their meaning is much closer if considered in the context of "house".

The test set contains approximately 12k pairs of phrases. A small public test set has been provided for testing purposes, but is not used in scoring.

Information on the meaning of CPC codes may be found on the [USPTO website](https://www.uspto.gov/web/patents/classification/cpc/html/cpc.html). The CPC version 2021.05 can be found on the [CPC archive website](https://www.cooperativepatentclassification.org/Archive).

Score meanings
The scores are in the 0-1 range with increments of 0.25 with the following meanings:

* 1.0 - Very close match. This is typically an exact match except possibly for differences in conjugation, quantity (e.g. singular vs. plural), and addition or removal of stopwords (e.g. “the”, “and”, “or”).
* 0.75 - Close synonym, e.g. “mobile phone” vs. “cellphone”. This also includes abbreviations, e.g. "TCP" -> "transmission control protocol".
* 0.5 - Synonyms which don’t have the same meaning (same function, same properties). This includes broad-narrow (hyponym) and narrow-broad (hypernym) matches.
* 0.25 - Somewhat related, e.g. the two phrases are in the same high level domain but are not synonyms. This also includes antonyms.
* 0.0 - Unrelated.

## Columns of the dataset
* **id** - a unique identifier for a pair of phrases
* **anchor** - the first phrase
* **target** - the second phrase
* **context** - the CPC classification (version 2021.05), which indicates the subject within which the similarity is to be scored
* **score** - the similarity. This is sourced from a combination of one or more manual expert ratings.

# Table of contents and short description
1. **basic-eda-and-data-preprocessing.ipynb** : Basic exploratory Data Analysis on the dataset is done.
2. **Roberta-model-approach.ipnyb** : Build the simple Roberta based NLP model. The Pearson Correlation coefficient for this model was 0.75. This saved model is used to build the web app, and the web app will be uploaded soon.
3. **new-tensorflow-deberta-v3-large-model-uspppm.ipynb** : This is the best performing NLP model which based on Deberta V3 Large model. The Pearson Correlation coefficient for this model was 0.8436. The more details about the model see the Jupyter Notebook.
4. **tf-deberta-v3large-phase2.ipynb** : This notebook we primarily use the saved model weights in **new-tensorflow-deberta-v3-large-model-uspppm.ipynb** for predicting the results for the test set.
5. **train** : the training set, containing phrases, contexts, and their similarity scores
6. **titles** : this dataset hold the description of each category in the **context** column
7. **test.csv** : the test set set, identical in structure to the training set but without the score
