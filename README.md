# Web APIs & NLP

---

### Problem Statement
Can we identify different keywords used by novice vs experts in the Engineering field and use them to predict subject matter difficulty level of a post?

---

### Executive Summary

The data used for testing this hypothesis is scraped from [Pushshift's](https://github.com/pushshift/api) API. Pushshift is a platform for collecting social media data for analysis. The data scraped from Reddit's Pushshift API is 1000 posts each from two subreddits r/explainlikeimfive and r/AskEngineers.

r/explainlikeimfive is a forum for layperson-friendly explanations. The content on this forum is for a novice in a field. On the other hand, r/AskEngineers is a forum for science and technology, and the content on this forum is for subject matter experts. There is a contrast in conceptual difficulty level. Since r/explainlikeimfive covers a wide array of topics, the data from this subreddit is narrowed down by using the search term `engineering`. Based on this, the posts from r/explainlikeimfive with search term engineering are compared with posts from r/AskEngineers.

Data Science work flow:
1. Data Acquisition - Scraping data from Reddit's Pushshift API from subreddits r/explainlikeimfive and r/AskEngineers.
2. Data Cleaning/Wrangling - Checking for integrity of data. Checking for missing values, in this case missing text.
3. Feature Engineering - In order to provide data to the model, the `title` and `selftext` columns are merged into `full_text`. Additionally, new columns are engineered like text length in `full_text_len`, word count in `full_text_word_count` and Sentiment Analysis.
4. Natural Language Processing - Since we are dealing with unstructured data, it is imperative to clean the data of special characters and turn it into tokens through a vectorizer.
5. Classification Modeling - After analyzing and determining the important features of the data, model is built using `Logistic Regression` and `Random Forest Classifier`. Numerical data is scaled through `Standard Scalar` and textual data is vectorized using `CountVectorizer`. The data is then combined and tuned using `FeatureUnion`, `Pipeline` and `GridSearchCV`. Each model is tuned for accuracy, precision and recall.

---

### Programming/Analytics Tools
- Pandas
- Numpy
- Matplotlib
- Seaborn
- Scikit-Learn
- CountVectorizer
- Logistic Regression
- Random Forest Classification

---

### Resources
- [`r/explainlikeimfive`](https://api.pushshift.io/reddit/search/submission?subreddit=explainlikeimfive&q=engineering)
- [`r/AskEngineers`](https://api.pushshift.io/reddit/search/submission?subreddit=AskEngineers)

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
| **senti_score_comp** | *float* | Compound polarity score



### Conclusion & Recommendations

Using data from Reddit's API, a classification model was built using Logistic Regression, with an accuracy of 93%. The model was able to achieve 92.5% precision and 93% recall. Another model was built using Random Forest Classifier. This model was rejected over the previous model for a low accuracy score, 92.7%.

Based on the Confusion Matrix, the number of False Positives (Type 1 Error) are 20 and number of False Negatives (Type 2 Error) are 16. Based on the application, it can be determined what kind of error need to be minimized. If a company is trying to attract novice readers, the company would want to minimize Type 1 Errors as it wants to encourage more readers.  

Amongst the top predictors for r/explainlikeimfive is engineering, which is obvious considering we used that as the search term. But some of the other top predictors are why, explain, how, explanation, difference, understand, reverse, computer and what. On the other hand, for r/AskScience, they are engineer, normal, advice, mechanical, degree, environmental, school, career, job, own, want. We can see a pattern in these words. The words from r/explainlikeimfive are more towards trying to understand things with why, how and what. Whereas, words from r/AskScience are more specific to the field.

It can be inferred that based on the words used in the posts, you can predict the subject matter expertise in the field and the difficulty level of the post.


As a future step, the model can be scaled and used to categorize articles on the level of subject matter difficulty, and can be used alongside *reading time* feature.

Additionally, it would be worth incorporating Decision Trees along with ensemble methods. Ensemble methods use multiple algorithms and make predictions on the target variable with better results as compared to individual algorithms. Boosting, AdaBoosting and Stacking could be considered for the model in future.
