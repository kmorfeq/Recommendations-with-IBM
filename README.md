# Recommendations-with-IBM

## Project Overview
I aim in my capstone to answer the following 2 questions:

  1. What are the top 10 most read articles
  2. 


## Problem Statement


## Data Exploration
The following is the schema for the tables that I'll use in this project:

### User Item Interactions Table
#### user-item-interactions.csv
  - article_id - the ID number of articles - float64
  - title - the titles of articles - object
  - email - email addresses of users who read the articles - object

Now, I'll list some of the content in the table to examine the table content

```python
# user-item-interactions.csv content 
df.head()
```

| __index__	  | __article_id__	| __title__	| __email__ |
|---------|------------|------------------------------------------------|------------------------------------------------|
|0	|1430.0	|using pixiedust for fast, flexible, and easier...	|ef5f11f77ba020cd36e1105a00ab868bbdbf7fe7|
|1	|1314.0	|healthcare python streaming application demo	|083cbdfa93c8444beaa4c5f5e0f5f9198e4f9e0b|
|2	|1429.0	|use deep learning for image classification	|b96a4f2e92d8572034b1e9b28f9ac673765cd074|
|3	|1338.0	|ml optimization using cognitive assistant	|06485706b34a5c9bf2a0ecdac41daf7e7654ceb7|
|4	|1276.0	|deploy your python model as a restful api	|f01220c46fc92c6e6b161b1849de11faacd7ccb2|


Since the other table has information about the articles, I'll identify the number of unique emails in the list and which email has read more articles than others

```python
# information about email column 
df.email.describe()
```
|  |  |
| --- | --- |
|__count__ |                                       45976 |
|__unique__|                                        5148|
|__top__  |     2b6c0f514c2f2b04ad3c4583407dccd0810469ee|
|__freq__ |                                          364|
|Name: email | dtype: object


### Articles Community Table
#### articles_community.csv
  - doc_body - content of articles - object
  - doc_description - description of articles - object
  - doc_full_name - articles full name - object
  - doc_status - articles status - object
  - article_id - the ID number of articles - float64
 
Now, I'll list some of the content in the table to examine the table content

```python
# articles_community.csv content
df_content.head()
```

| __index__	| __doc_body__ |	__doc_description__ |	__doc_full_name__ |	__doc_status__ |	__article_id__ |
|---------|-----------------------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------|-------------|-------|
|0	|Skip navigation Sign in SearchLoading...\r\n\r...	|Detect bad readings in real time using Python ...	|Detect Malfunctioning IoT Sensors with Streami...	|Live|	0|
|1	|No Free Hunch Navigation * kaggle.com\r\n\r\n ...	|See the forest, see the trees. Here lies the c...	|Communicating data science: A guide to present...	|Live|	1|
|2	|☰ * Login\r\n * Sign Up\r\n\r\n * Learning Pat...	|Here’s this week’s news in Data Science and Bi...	|This Week in Data Science (April 18, 2017)	|Live|	2|
|3	|DATALAYER: HIGH THROUGHPUT, LOW LATENCY AT SCA...	|Learn how distributed DBs solve the problem of...	|DataLayer Conference: Boost the performance of...	|Live|	3|
|4	|Skip navigation Sign in SearchLoading...\r\n\r...	|This video demonstrates the power of IBM DataS...	|Analyze NY Restaurant data using Spark in DSX	|Live|	4|
