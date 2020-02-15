# Recommendations-with-IBM
This capstone project is part of the Data Science Nanodegree by Udacity

## Project Overview
I aim in my capstone to built a recommendation engine to recommend articles for users, either new users or existings.
And part of the project, I'll answer the following 2 questions:

  1. What are the top 10 most read articles
  2. What are the recommended articles for new users


## Problem Statement


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
print('Number of Unique articles is: ', df.groupby('article_id')['email'].nunique().sort_values(ascending=False).count())

# identify total number of aricles
print('Total number of articles on the IBM platform: ', df_content['article_id'].nunique(dropna = True))

# identify number of unique users
print('Number of unique users: ', df['email'].nunique(dropna=True))

# identify number of user-article interactions
print('Number of user_article interaction: ', df.count()[0])
```
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
