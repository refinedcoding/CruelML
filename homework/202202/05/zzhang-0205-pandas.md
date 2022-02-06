### Pandas

##### Crete

- Dataframe

```python
pd.DataFrame({'Bob': ['I liked it.', 'It was awful.'], 
              'Sue': ['Pretty good.', 'Bland.']},
             index=['Product A', 'Product B'])
```

- Series

```python
pd.Series([30, 35, 40], 
					index=['2015 Sales', '2016 Sales', '2017 Sales'], 
					name='Product A')
```



##### Read

- read csv

```python
wine_reviews = pd.read_csv("../input/wine-reviews/name.csv")
```



##### Write

- write to csv

```python
animals = pd.DataFrame({'Cows': [12, 20], 'Goats': [22, 19]}, index=['Year 1', 'Year 2'])
animals.to_csv("cows_and_goats.csv")
```



##### Read with `loc` and `iloc`

- 用`iloc`，是不包含右值的，跟普通的一样，用`loc`是包含右值的

- `iloc`: 0:10 means 0,...,9
- `loc`: 0:10 means 0,...,10



##### Summary Functions

```python
reviews.points.desribe()
reviews.points.mean()
reviews.taster_name.unique() # view a list of unique values
reviews.taster_name.value_counts() # view a list of unique values and how often they occur in the dataset,
```



##### Map

```python
review_points_mean = reviews.points.mean()
reviews.points.map(lambda p: p - review_points_mean)
```



##### Apply

```python
review_points_mean = reviews.points.mean()
reviews.points.map(lambda p: p - review_points_mean)
```



##### Groupwise analysis

```python
reviews.groupby('points').points.count()
reviews.groupby('points').price.min()
reviews.groupby('winery').apply(lambda df: df.title.iloc[0])
reviews.groupby(['country', 'province']).apply(lambda df: df.loc[df.points.idxmax()]) # pick out the best wine by country and province
reviews.groupby(['country']).price.agg([len, min, max]) # add three new columns
```



##### Missing data

```python
reviews[pd.isnull(reviews.country)]
reviews.region_2.fillna("Unknown")
reviews.taster_twitter_handle.replace("@kerinokeefe", "@kerino")
```



##### Rename

```python
reviews.rename(columns={'points': 'score'})
reviews.rename(index={0: 'firstEntry', 1: 'secondEntry'})
reviews.rename_axis("wines", axis='rows').rename_axis("fields", axis='columns')
```



##### Combine two tables

```python
left = canadian_youtube.set_index(['title', 'trending_date'])
right = british_toutube.set_index(['title', 'trending_date'])

left.join(right, lsuffix='_CAN', rsuffix='_UK')
```

