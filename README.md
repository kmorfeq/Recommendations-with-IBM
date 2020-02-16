# Recommendations-with-IBM
This capstone project is part of the Data Science Nanodegree by Udacity

## Project Overview
I aim in my capstone to built a recommendation engine to recommend articles for users, either new users or existings.
And part of the project, I'll answer the following 2 questions:

  1. What are the top 10 most read articles
  2. What are the recommended articles for new users


## Problem Solving Strategy
To build the recommendation engine, I'll follow the following steps:
1. Load datasets ( in this project, I've two csv file )
2. explore the datasets to gather some insights
3. clean the datasets, either drop or replace the un-needed values.
4. Build recommendation engines


## Data Exploration
The following is the schema for the tables that I'll use in this project:

### User Item Interactions Table
#### user-item-interactions.csv
  - article_id - the ID number of articles - float64
  - title - the titles of articles - object
  - email - email addresses of users who read the articles - object


| __index__	  | __article_id__	| __title__	| __email__ |
|---------|------------|------------------------------------------------|------------------------------------------------|
|0	|1430.0	|using pixiedust for fast, flexible, and easier...	|ef5f11f77ba020cd36e1105a00ab868bbdbf7fe7|
|1	|1314.0	|healthcare python streaming application demo	|083cbdfa93c8444beaa4c5f5e0f5f9198e4f9e0b|
|2	|1429.0	|use deep learning for image classification	|b96a4f2e92d8572034b1e9b28f9ac673765cd074|
|3	|1338.0	|ml optimization using cognitive assistant	|06485706b34a5c9bf2a0ecdac41daf7e7654ceb7|
|4	|1276.0	|deploy your python model as a restful api	|f01220c46fc92c6e6b161b1849de11faacd7ccb2|


### Articles Community Table
#### articles_community.csv
  - doc_body - content of articles - object
  - doc_description - description of articles - object
  - doc_full_name - articles full name - object
  - doc_status - articles status - object
  - article_id - the ID number of articles - float64
 

| __index__	| __doc_body__ |	__doc_description__ |	__doc_full_name__ |	__doc_status__ |	__article_id__ |
|---------|-----------------------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------|-------------|-------|
|0	|Skip navigation Sign in SearchLoading...\r\n\r...	|Detect bad readings in real time using Python ...	|Detect Malfunctioning IoT Sensors with Streami...	|Live|	0|
|1	|No Free Hunch Navigation * kaggle.com\r\n\r\n ...	|See the forest, see the trees. Here lies the c...	|Communicating data science: A guide to present...	|Live|	1|
|2	|☰ * Login\r\n * Sign Up\r\n\r\n * Learning Pat...	|Here’s this week’s news in Data Science and Bi...	|This Week in Data Science (April 18, 2017)	|Live|	2|
|3	|DATALAYER: HIGH THROUGHPUT, LOW LATENCY AT SCA...	|Learn how distributed DBs solve the problem of...	|DataLayer Conference: Boost the performance of...	|Live|	3|
|4	|Skip navigation Sign in SearchLoading...\r\n\r...	|This video demonstrates the power of IBM DataS...	|Analyze NY Restaurant data using Spark in DSX	|Live|	4|


Some information about the datasets.

```python
# identify number of unique articles with at least one interaction
Number of Unique articles is:  714
# identify total number of aricles
Total number of articles on the IBM platform:  1051
# identify number of unique users
Number of unique users:  5148
# identify number of user-article interactions
Number of user_article interaction:  45993
```

## Data Visualization
The following are some results from the project:

### Duplicated article_id in the Articles Community Table

| __index__	| __doc_body__ |	__doc_description__ |	__doc_full_name__ |	__doc_status__ |	__article_id__ |
|---------|-----------------------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------|-------------|-------|
|365	|Follow Sign in / Sign up Home About Insight Da...	|During the seven-week Insight Data Engineering...	|Graph-based machine learning	|Live	|50
|692	|Homepage Follow Sign in / Sign up Homepage * H...	|One of the earliest documented catalogs was co...	|How smart catalogs can turn the big data flood...	|Live	|221
|761	|Homepage Follow Sign in Get started Homepage ...	|Today’s world of data science leverages data f...	|Using Apache Spark as a parallel processing fr...	|Live	|398
|970	|This video shows you how to construct queries ...	|This video shows you how to construct queries ...	|Use the Primary Index	|Live	|577
|971	|Homepage Follow Sign in Get started * Home\r\n...	|If you are like most data scientists, you are ...	|Self-service data preparation with IBM Data Re...	|Live	|232

### User Item Interaction table after replacing email with user_id
| __index__	  | __article_id__	| __title__	| __user_id__ |
|---------|------------|------------------------------------------------|------------------------------------------------|
|0	|1430.0	|using pixiedust for fast, flexible, and easier...	|1
|1	|1314.0	|healthcare python streaming application demo	|2
|2	|1429.0	|use deep learning for image classification	|3
|3	|1338.0	|ml optimization using cognitive assistant	|4
|4	|1276.0	|deploy your python model as a restful api	|5

### Top articles read by users
![GitHub Logo](/pic/Top10articles.png)

### The top 10 recommendations for user_id (20)
| #  | __article_id__	| __title__	|
|---|------|----------------------------------------------------|
|0    |1429.0 |healthcare python streaming application demo|
|1    |1330.0 |analyze energy consumption in buildings|
|2    |1431.0 |use xgboost, scikit-learn & ibm watson machine learning apis|
|3    |1427.0 |deep learning with tensorflow course by big data university|
|4    |1364.0 |visualize car data with brunel|
|5    |1314.0 |predicting churn with the spss random tree algorithm|
|6    |1162.0 |gosales transactions for logistic regression model|
|7    |1304.0 |insights from new york car accident reports|
|8    |  43.0 |model bike sharing data with spss|
|9    |1351.0 |use deep learning for image classification|

### Accuracy of the recommendation engine
![GitHub Logo](/pic/accuracy.png)


## Blogpost
http://github.com - automatic!
