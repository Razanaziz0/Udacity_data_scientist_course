# Udacity_data_scientist_course

## Seattle Airbnb

Since 2008, guests and hosts have used Airbnb to travel in a more unique, personalized way. As part of the Airbnb Inside initiative, this dataset describes the listing activity of homestays in Seattle, WA.

The following Airbnb activity is included in this Seattle dataset:

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
