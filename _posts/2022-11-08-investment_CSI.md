---
layout: post
title:  "Finding good financial instruments with consumer sentiment index data"
---

# This project intended to find the relationship between return rate of financial instruments and consumer sentiment index and found out there was no meaningful relation.
**This project used API, NoSQL, MongoDB, Flask, Regression models and Pickling.**

### Data
- Rate of return for each funds and consumer sentiment index(CSI) data has been downloaded from two sources

|Data set|Source|Type|
|---|---|---|
|Return rate of funds|Integrated pension portal of Financial Supervisory Service|JSON (API)|
|Consumer sentiment index (CSI)|Statistics Korea website|CSV|

- Data set has been retrieved from Financial Supervisory Service through API. Then, the data is loaded to database (MongoDB)
<img src="/assets/CodeStatesSection3/MongoDB.png" width="80%">
- Below is the code to use API and load to MongoDB

```python
import time
import copy
import requests
from pymongo import MongoClient
import json

key = ''
areaCode =3

## 2019-4Q data set
year = 2019
quarter = 4

url = f"https://100lifeplan.fss.or.kr/openapi/api/psProdList.json?key={key}&year={year}&quarter={quarter}"

data = ''
data_list =[]

response = requests.get(url)
time.sleep(1)

if response.status_code ==200:
    data = response.json()
    data_list = copy.deepcopy(data)


## MongoDB 2019-4Q

HOST = 'cluster0.o1n9upq.mongodb.net'
USER = 'Codestates_Jihye'
PASSWORD = ''
DATABASE_NAME = "Financial_Supervisory_Service_Pension"
COLLECTION_NAME = "2019_4Q"
MONGO_URI = f"mongodb+srv://{USER}:{PASSWORD}@{HOST}/{DATABASE_NAME}?retryWrites=true&w=majority"

client = MongoClient(MONGO_URI)
database = client[DATABASE_NAME]
collection = database[COLLECTION_NAME]
collection.insert_one(data_list)

```


### Model


### Result


### Tools
