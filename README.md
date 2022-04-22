# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png)   Web APIs & NLP

---

### Description
Created a **classification model** for **unstructured data**. Used the model to predict what subreddit posts belong to. Used data(posts) from two subreddits **r/explainlikeimfive** and **r/AskEngineers**. 

---

### Problem Satement
Can we identify different keywords used by novice vs experts in Engineering and use it to predict subject matter difficulty level of a post? 

---

### Summary 
The dataset used for testing this hypothesis is scraped from [Pushshift's](https://github.com/pushshift/api) API. Pushshift is a platform for collecting social media data for analysis. The data scraped from Reddit's Pushshift API is 1000 posts each from two subreddits r/explainlikeimfive and r/AskEngineers.

r/explainlikeimfive is a forum for layperson-friendly explanations. The content on this forum is for a novice in the field. This forum has On the other hand, r/AskEngineers is a forum for science and technology, and the content on this forum is for subject matter experts. There is contrast in the conceptual difficulty level. Because r/explainlikeimfive is a large unbrella, under which a lot of topics are covered, I narrowed down my data from this subreddit to the search term 'engineering'. Based on this, I am comparing the posts from r/explainlikeimfive with search term engineering with posts from r/AskEngineers. 

Following are the steps involved for achieving the goal: 
1. Data Wrangling/Gathering/Acquisition - Scrapping the data from Reddit's Pushshift API. 
2. Data Cleaning - Checking for the integrity of the data. Checking for missing values, in this case missing text. 
3. Natural Language Processing - As we are dealing with unstructured data, it is important to structure the data. This involves cleaning the data of special characters. Additionally, turning the text into tokens for lemmatizing or stemming it. 
3. Exploratory Data Analysis - In this case, exploratory analysis involves checking the text length, word count, categorization and distribution. 
4. Classification Modeling - After analyzing and determining the important features of the data comes building a model, and using train and test datasets train and test the model perfomance. The train dataset is transformed from text to numbers using CountVectorizer. Taking the vectorized data and numerical data, a classification model (Logistic Regression) is built. GridSearchCV is used to determine the best model parameters. It's predictions are compared to the test dataset.

---

### Programming/Analytics Tools
- Pandas
- Numpy
- Matplotlib
- Seaborn
- Scikit-Learn
- CountVectorizer
- Logistic Regression 
- RandomForest Classification

--- 

### Resources
- [`r/explainlikeimfive`]https://api.pushshift.io/reddit/search/submission?subreddit=explainlikeimfive&q=engineering
- [`r/AskEngineers`]https://api.pushshift.io/reddit/search/submission?subreddit=AskEngineers

---

### Data Dictionary

|Feature|Type|Description|
| --- | --- | --- |
| **title** | *object* | Title of the posts/submissions 
| **selftext** | *object* | Body of the posts
| **subreddit** | *int* | Name of the subreddit that the post belongs to. r/AskEngineers: 0, r/explainlikeimfive: 1
| **full_text** | *object*  |Text from title and selftext combined
| **created_utc** | *int* | Time the post was created
| **full_text_len** | *int* | Length of full_text 
| **full_text_word_count** | *int* | Word count of full_text



### Conclusion & Recommendations 

Using data from Reddit's API, a classification model is built using Count Vectorizer and Logistic Regression, with an accuracy of 93%. Another model using the same data was built using Count Vectorizer and Roandom Forrest Classifier. This model was rejected over the previous model as due to a comparatively low accuracy score, 92.7%. 

Based on the Confusion Matrix, the number of False Positives are 20 and number of False Negatives are 16. The False Positives are Type 1 Errors and False Negatives are Type 2 Errors. Based on the application, it can be determined what kind error needs to be minimized. A real world application for this model would be categorizing a blog post for novice or expert. This could be an addition alongside *reading time* feature. If a company is trying to attract readers who are not subject matter experts, the company would want to minimize Type 1 Errors as it wants to encourage more readers.  

Amongst the top predictors for r/explainlikeimfive is engineering, which is obvious considering we used that as the search term. But some of the other top predictors are why, explain, how, explanation, difference, understand, reverse, computer and what. On the other hand, for r/AskScience, they are engineer, normal, advice, mechanical, degree, environmental, school, career, job, own, want. We can definitely see a pattern in these words. The words from r/explainlikeimfive are more towards trying to understand things with why, how and what. Whereas, words from r/AskScience are more specific to the field. 

It can be pointed out that based on the words used in the posts, you can predict the subject matter expertise in the field and the difficulty level of the post. 

As a future step, it would be worth to further explore Decision Trees along with ensemble methods. Ensemble methods use multiple algorithms and make predictions on the target variable with better results as compared to individual algorithms. Boosting, AdaBoosting and Stacking could be considered for the model in future. 








