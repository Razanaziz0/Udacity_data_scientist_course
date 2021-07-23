# Airbnb Seattle Analysis

This is the project of Udacity's data scientist nanodegree program

## Analysis Airbnb Seattle Data By CRISP-DM Process
CRISP-DM  process(Cross-Industry Standard Process for Data Mining): is a process model describing the life cycle of data science. In short, it guides you through the entire phases of planning, organizing, and implementing your data mining project.
## CRISP-DM process majors.

1-Business Understanding

2-Data Understanding

3-Data Preparation

4-Modeling

5-Evaluation

6-Deployment

### 1-Business Understanding
An Airbnb is a residential property that hosts rent on a short term basis to travelers. It can be anything from a house, a single room, a boat or even a tree house. Think of it as pop-up accommodation – a market place where people rent out their properties.


after I understand the busness I considered three below questions to explore its way.

1-When do reservations increase in Seattle?

2-If bookings increase is prices increase ?

3-what's the room prices based on neighborhoods ?

We can be able to answer these questions by analysing Airbnb dataset.


### 2-Data Understanding
We have three  Airbnb dataset:

1-Listings, including full descriptions and average review score

2- including unique id for each reviewer and detailed comments

3-Calendar, including listing id and the price and availability for that day


```python
import requests
import pandas as pd
import numpy as np
import datetime as dt
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import r2_score, mean_squared_error
import ImputingValues as t
import seaborn as sns
```

```python
calendar = pd.read_csv('C:/Users/AlmousaRazan/Downloads/archive/calendar.csv')
listings = pd.read_csv('C:/Users/AlmousaRazan/Downloads/archive/listings.csv')
reviews = pd.read_csv('C:/Users/AlmousaRazan/Downloads/archive/reviews.csv')

```

```python



calendar.columns
calendar.head()
calendar.dtypes
```



```python
calendar['listing_id']=calendar['listing_id'].astype('str')
calendar['price'] = calendar['price'].str.replace('[\$,]', '')

sample=calendar.head(10000)

calendar['price'] = pd.to_numeric(calendar['price'])
calendar['date']=pd.to_datetime(calendar['date'])

calendar_dropna = calendar.dropna(axis=0)
calendar_dub=calendar_dropna.drop_duplicates(keep = 'first')
calendar_dub['cnt']=1
calendar_group= calendar_dub.groupby(['date'], as_index=False)['price'].mean()
calendar_group2= calendar_dub.groupby(['date'], as_index=False)['cnt'].sum()
calendar_group.dtypes
month = calendar_group.date.dt.month.unique()

sns.barplot(calendar_group.date.dt.month,calendar_group['price']);
plt.title('date price');

```
