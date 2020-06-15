# Learn2Relax
Stress Detection in Social Media. <br>Here is my [prensentation](https://docs.google.com/presentation/d/1iZFROfJrI9I-OIB1vEbSchwLOnL0VAU-T9Yg5wtN2lM/edit#slide=id.p).

## Motivation for this project
Social media is a major platform where people express their worries and stresses across the world. The project was built in order to analyze content and identify stress from reddit data by deploying NLP techniques. Supervised learning with pre-trained word embeddings was deployed on unlabled data by both discrete and neural models. 

## Requisites
- MacOS or Linux
- Python 3.7.4
- conda 
- pip

## Setup
This project requires Python 3.7.4 and conda environment. To setup the environment, please follow these steps:

- Create a new conda virtual environment in local or cloud services
```
conda create -n new_env python=3.7.4 
conda activate new_env 
```
- Clone the github repository
```
https://github.com/Evaaaaaaa/Learn2Relax.git
```
- Install the required packages in the conda environment
```
cd Learn2Relax/build
pip install -r requirements.txt
```
- Download nltk data packages
```
python Learn2Relax/configs/config.py
```
### Additional Setup
- Install tensorflow for GPU to run BERT model on GPU
```
pip install tensorflow-gpu==1.15
```

## Data
Labeleded data is retrieved from [Dreaddit: A Reddit Dataset for Stress Analysis in Social Media](https://arxiv.org/abs/1911.00133). 

Picture below shows words similarities in the dataset.
<img src="figs/similar_words.png" width="1000">

Top 20 frequent words in stressed posts and non-stressed posts are shown below.

<img src="figs/Top_20_words.png" width="1000">


## Analysis
Features for the labeled dataset were generated by five different feature extraction methods:<br> unigram TF-IDF, bigram TF-IDF, Word2Vec with TF-IDF as weights and BERT embeddings. 

Word2Vec embeddings were also trained with 190k unlabeled Reddit posts. 

After feature extraction, 9 classification models were trained: <br>Logistic regression, Naive Bayes, SVM, AdaBoost, Gradient Boosting, Decision Tree, Random forest, XGBoost and BERT. 

### Results
|Featurization Method|Best Model|Accuracy|Precision|Recall|F1-Score|
|:-------------|:----------|:--------|:---------|:------|:--------|
|Unigram TF-IDF|Logistic Regression|84.23%  |82.87%   |90.36%|86.46%  |
|Bigram TF-IDF|SVM       |84.23%  |83.24%   |89.76%|86.38%  |
|Word2Vec + TF-IDF|XGBoost   |85.23%  |82.80%   |92.77%|87.50%  |
|Pretrained Embeddings|XGBoost   |84.56%  |81.58%   |93.37%|87.08%  |
|BERT Embeddings|BERT      |92.74%  |92.90%   |94.58%|93.73%  |

<img src="figs/supervised_results.png" width="650">

- Recall is the most important metric here because we want to predict as more stress posts accurately as possible, as well as prevent misclassifying non-stress posts as stressful.

- BERT is the most robust model with all four metrics the highest.
- All models are able to provide a confidence score in addition to prediction.

## Reference
- [[NLP] Performance of Different Word Embeddings on Text Classification](https://towardsdatascience.com/nlp-performance-of-different-word-embeddings-on-text-classification-de648c6262b)
- [Predicting Movie Reviews with BERT on TF Hub](https://colab.research.google.com/github/google-research/bert/blob/master/predicting_movie_reviews_with_bert_on_tf_hub.ipynb)

