# News article classification

## Summary
A custom-built NLP dataset of news articles labelled by topic, created with calls to the Guardian API and BeautifulSoup, is used to train and validate a text classifier. The model is then deployed for inference as a web application using Dash.

## Set-up
No special hardware is needed for all the code in this repo. However, in order to seamlessly reproduce the workflow, you might want to exploit the custom conda environment in `environment.yml` by running the following:

```
$ git clone git@github.com:mz256/Guardian_news_classification.git
$ cd Guardian_news_classification
$ conda env create
$ conda activate nlp-env
```

## Description

1. The script `01_scrape_guardian` exploits the Guardian Open Platform API and BeautifulSoup to scrape and parse news articles about a collection of chosen topics (environment, business, film, culture and education). These are then organised and saved as a dataset for analysis. NB: `00_scrape_guardian_test` is a more descriptive step-by-step walkthrough of the scraping process used (this time on news about elections in Hong Kong).

2. `02_preprocess` then performs EDA and preprocessing of the data gathered in the previous step. Duplicate entries are removed and the topic distributions of article number or length are obtained, to determine a viable model building and testing strategy for classification. Data is then cleaned and processed in a standard way (lowercase, tokenise, remove stop-words and punctuation, lemmatise) using the default English pipeline from spaCy. Finally, the tokens are numericalised as TF-IDF vectors.

3. Three different models (SVM, multinomial Naive Bayes and Random Forest) are trained and chosen subsets of their hyperparameters are tuned using randomised search 3-fold cross-validation for speed. Accuracy is used as the CV metric, as the classes are balanced. In all cases, the best cross-validated model is then re-trained on the whole training set for better generalisation. In addition to accuracy, other more descriptive metrics (Precision, Recall and F1) or visualisations (confusion matrix) are inspected at this stage in order to gauge model performance on the test set. The SVM is chosen as the best-performing model for our dataset.

4. In `06_deployment`, the model is embedded in a web application written with Dash and deployed locally. The UI lets the user choose between manually inserting a short sentence or scraping a number of fresh news articles. The model predicts the most likely topic of discussion and results are displayed.

