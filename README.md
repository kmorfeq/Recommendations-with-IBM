# Recommendations-with-IBM

## Project Overview
I aim in my capstone to answer the following 2 questions:

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

Identify number of null values in each column

```python
df.isna().sum()
```
|__column name__ | __Number of Nulls__ |
|-----|-----|
|article_id    | 0|
|title          |0|
|email         |17|

The only null values were in the email column which means there are 17 articles ( or less since there are duplicates ) were not read by any user.

Since the other table has information about the articles, I'll identify the number of unique emails in the list and which user has read more articles than others

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

As we can see above, there are 5148 unique email in the table. And the email that read the most article is `2b6c0f514c2f2b04ad3c4583407dccd0810469ee` with 364 read articles.


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

We can see that some of the content in the doc_body column need some cleaning or correction such in row 2 where there is \r\n in content. But since it'll not impact my findings, it'll not be corrected nor deleted.

Now, we need to Identify number of null values in df_content table to check if dropping rows is needed.

```python
df_content.isna().sum()
```
|__column name__ | __Number of Nulls__ |
|-----|-----|
|doc_body           |14
|doc_description     |3
|doc_full_name       |0
|doc_status          |0
|article_id          |0


Next, I'll check if there is any duplicate articles in df_content table.

```python
# Find and explore duplicate articles
filt = df_content.duplicated(['article_id'], keep='first')
df_content.loc[filt]
```
| __index__	| __doc_body__ |	__doc_description__ |	__doc_full_name__ |	__doc_status__ |	__article_id__ |
|---------|-----------------------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------|-------------|-------|
|365 	|Follow Sign in / Sign up Home About Insight Da... 	|During the seven-week Insight Data Engineering... 	|Graph-based machine learning 	|Live 	|50
|692 	|Homepage Follow Sign in / Sign up Homepage * H... 	|One of the earliest documented catalogs was co... 	|How smart catalogs can turn the big data flood... 	|Live 	|221
|761 	|Homepage Follow Sign in Get started Homepage *... 	|Today’s world of data science leverages data f... 	|Using Apache Spark as a parallel processing fr... 	|Live 	|398
|970 	|This video shows you how to construct queries ... 	|This video shows you how to construct queries ... 	|Use the Primary Index 	|Live 	|577
|971 	|Homepage Follow Sign in Get started * Home\r\n... 	|If you are like most data scientists, you are ... 	|Self-service data preparation with IBM Data Re... 	|Live 	|232

we can see that only five articles are duplicated at least once, as above table. Nest step will be to drop all the duplicated and just keep the first enteries.

```python
# Remove any rows that have the same article_id - only keep the first
df_content.drop_duplicates('article_id', keep='first', inplace=True)
```

After dropping the duplicates, I'll identify some information about the datasets.

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
