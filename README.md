![#0b155e](https://via.placeholder.com/600x100/0b155e/FFFFFF/?text=Project+3)

# Web Scraping and Natural Language Processing


## Hypothesis
---

$H_0$ = There is no difference in what people post on the Nikon and Canon subreddit and cannot be distinguished.

$H_A$ =There is a difference between posts and those differences can be used to identify the origin.


## Executive Summary
---
In this project, I scraped data from two sub reddits with the use of an API, cleaned the data, vectorized it and modeled it.  The intention of this process was to see if the model could accurately predict which sub reddit that any particular post came from based on the content in the post.  For this analysis, I ran several combinations of vectorizers and modelers to find the most accurate model.

**BLUF:** Based a few keywords you can deterimine the origin of a post with over 90% accuracy.

## Data 
---
The data for this project was scraped from reddit.com using the Pushshift API.  Three subreddits were targeted: r/canon, r/Nikon, r/SonyAlpha.  While this analysis will focus primarily on Canon and Nikon, the Sony data was scraped for potential project expansion in the future.  For each manufacturer I pulled a total of 1,000 posts.  

## Findings
---
#### ![#f03c15](https://via.placeholder.com/20/f03c15/f03c15?text=.) Model 1 : 
**Count Vectoirzer and Logistic Regression on Title Text**

**Results:**

After a five fold Grid Seach the best parameters for this model:

`cvec__max_features = 1,000`
`cvec__ngram_range = (1, 1)`
`cvec__stop_words = english`

These parameters resulted in a model that scored a .97 on the training data, but only .89 on the testing data.  This indicates variance in the model.  To be clear, a .89 is still a good score and demonstrates a very predictive model.  The most predicitve words in this model were "card" and "bird", which both had odds over 10 to predict a Canon post.

#### ![#3c2696](https://via.placeholder.com/20/3c2696/3c2696?text=.) Model 2 :
**TFIDF Vectoirzer and Bernoulli Naive Bays on Title Text**

After a five fold Grid Seach the best parameters for this model:

`cvec__max_features = 500`
`cvec__ngram_range = (1, 1)`
`cvec__stop_words = english`

These parameters resulted in a model that scored a .91 on the training data, but only .89 on the testing data.  While this model did not preform as well overall, it much lower variance.  Similar to the previous model, there is a very high predictive quality based on the scores.

#### ![#a31d74](https://via.placeholder.com/20/a31d74/a31d74?text=.) Model 3 :
**Count Vectoirzer and Logistic Regression on Combination Text**

After a five fold Grid Seach the best parameters for this model:

`cvec__max_features = 1,000`
`cvec__ngram_range = (1, 1)`
`cvec__stop_words = none`

These parameters resulted in a model that scored a .985 on the training data, but only .913 on the testing data.  This is by far the best perfroming model of the three.  This can be attributed the increased amount of text data from the body of the posts.   The most predicitve words in this model were "price" and "gets", which both had odds over 9 to predict a Canon post.

## Project Organization
---
```
project-directory
|__ code
|   |__ 01_Obtain_Data
|   |__ 02_EDA_and_Cleaning.ipynb   
|   |__ 03_Model.ipynb    
|__ data
|   |__ canon_merge.csv
|   |__ canon1.csv
|   |__ canon2.csv
|   |__ nikon_merge.csv
|   |__ nikon1.csv
|   |__ nikon2.csv
|   |__ photo.csv
|   |__ sony_merge.csv
|   |__ sony1.csv
|   |__ sony2.csv
|__ Project_3_presentation.pdf
|__ README.md
```