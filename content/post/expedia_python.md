+++
date = "2017-01-27T23:05:56-05:00"
title = "Expedia kaggle competition"
draft = "true"
categories = ["misc"]

+++

```python
import pandas as pd
destinations = pd.read_csv("../data/destinations.csv")
test = pd.read_csv("../data/test.csv")
train = pd.read_csv("../data/train.csv")
```


```python
train.shape
```
    (37670293, 24)

```python
test.shape
```
    (2528243, 22)


```python
train.head(5)
```

<div>
<table border="1" class="dataframe" >
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date_time</th>
      <th>site_name</th>
      <th>posa_continent</th>
      <th>user_location_country</th>
      <th>user_location_region</th>
      <th>user_location_city</th>
      <th>orig_destination_distance</th>
      <th>user_id</th>
      <th>is_mobile</th>
      <th>is_package</th>
      <th>...</th>
      <th>srch_children_cnt</th>
      <th>srch_rm_cnt</th>
      <th>srch_destination_id</th>
      <th>srch_destination_type_id</th>
      <th>is_booking</th>
      <th>cnt</th>
      <th>hotel_continent</th>
      <th>hotel_country</th>
      <th>hotel_market</th>
      <th>hotel_cluster</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014-08-11 07:46:59</td>
      <td>2</td>
      <td>3</td>
      <td>66</td>
      <td>348</td>
      <td>48862</td>
      <td>2234.2641</td>
      <td>12</td>
      <td>0</td>
      <td>1</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>8250</td>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
      <td>50</td>
      <td>628</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2014-08-11 08:22:12</td>
      <td>2</td>
      <td>3</td>
      <td>66</td>
      <td>348</td>
      <td>48862</td>
      <td>2234.2641</td>
      <td>12</td>
      <td>0</td>
      <td>1</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>8250</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>50</td>
      <td>628</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2014-08-11 08:24:33</td>
      <td>2</td>
      <td>3</td>
      <td>66</td>
      <td>348</td>
      <td>48862</td>
      <td>2234.2641</td>
      <td>12</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>8250</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>50</td>
      <td>628</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2014-08-09 18:05:16</td>
      <td>2</td>
      <td>3</td>
      <td>66</td>
      <td>442</td>
      <td>35390</td>
      <td>913.1932</td>
      <td>93</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>14984</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>50</td>
      <td>1457</td>
      <td>80</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014-08-09 18:08:18</td>
      <td>2</td>
      <td>3</td>
      <td>66</td>
      <td>442</td>
      <td>35390</td>
      <td>913.6259</td>
      <td>93</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>1</td>
      <td>14984</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>50</td>
      <td>1457</td>
      <td>21</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 24 columns</p>
</div>



```python
test.head(5)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>date_time</th>
      <th>site_name</th>
      <th>posa_continent</th>
      <th>user_location_country</th>
      <th>user_location_region</th>
      <th>user_location_city</th>
      <th>orig_destination_distance</th>
      <th>user_id</th>
      <th>is_mobile</th>
      <th>...</th>
      <th>srch_ci</th>
      <th>srch_co</th>
      <th>srch_adults_cnt</th>
      <th>srch_children_cnt</th>
      <th>srch_rm_cnt</th>
      <th>srch_destination_id</th>
      <th>srch_destination_type_id</th>
      <th>hotel_continent</th>
      <th>hotel_country</th>
      <th>hotel_market</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>2015-09-03 17:09:54</td>
      <td>2</td>
      <td>3</td>
      <td>66</td>
      <td>174</td>
      <td>37449</td>
      <td>5539.0567</td>
      <td>1</td>
      <td>1</td>
      <td>...</td>
      <td>2016-05-19</td>
      <td>2016-05-23</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>12243</td>
      <td>6</td>
      <td>6</td>
      <td>204</td>
      <td>27</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2015-09-24 17:38:35</td>
      <td>2</td>
      <td>3</td>
      <td>66</td>
      <td>174</td>
      <td>37449</td>
      <td>5873.2923</td>
      <td>1</td>
      <td>1</td>
      <td>...</td>
      <td>2016-05-12</td>
      <td>2016-05-15</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>14474</td>
      <td>7</td>
      <td>6</td>
      <td>204</td>
      <td>1540</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>2015-06-07 15:53:02</td>
      <td>2</td>
      <td>3</td>
      <td>66</td>
      <td>142</td>
      <td>17440</td>
      <td>3975.9776</td>
      <td>20</td>
      <td>0</td>
      <td>...</td>
      <td>2015-07-26</td>
      <td>2015-07-27</td>
      <td>4</td>
      <td>0</td>
      <td>1</td>
      <td>11353</td>
      <td>1</td>
      <td>2</td>
      <td>50</td>
      <td>699</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>2015-09-14 14:49:10</td>
      <td>2</td>
      <td>3</td>
      <td>66</td>
      <td>258</td>
      <td>34156</td>
      <td>1508.5975</td>
      <td>28</td>
      <td>0</td>
      <td>...</td>
      <td>2015-09-14</td>
      <td>2015-09-16</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>8250</td>
      <td>1</td>
      <td>2</td>
      <td>50</td>
      <td>628</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>2015-07-17 09:32:04</td>
      <td>2</td>
      <td>3</td>
      <td>66</td>
      <td>467</td>
      <td>36345</td>
      <td>66.7913</td>
      <td>50</td>
      <td>0</td>
      <td>...</td>
      <td>2015-07-22</td>
      <td>2015-07-23</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>11812</td>
      <td>1</td>
      <td>2</td>
      <td>50</td>
      <td>538</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>




```python
train["hotel_cluster"].value_counts()
```




    91    1043720
    41     772743
    48     754033
    64     704734
    65     670960
    5      620194
    98     589178
    59     570291
    42     551605
    21     550092
    70     545572
    18     545284
    83     534132
    46     534038
    25     530591
    62     518809
    95     509266
    28     507016
    68     503797
    82     503755
    37     496061
    50     489892
    30     489287
    9      488328
    58     483253
    97     479446
    16     477868
    72     457463
    1      452694
    99     444887
           ...   
    19     282893
    84     278264
    66     273505
    38     269246
    87     260398
    23     259233
    12     259022
    31     257587
    67     255946
    43     253578
    7      252447
    54     250745
    92     244343
    89     243560
    45     241408
    49     240124
    3      225250
    80     220218
    60     217919
    71     216054
    93     214293
    86     209054
    14     192299
    75     165226
    24     164127
    35     139122
    53     134812
    88     107784
    27     105040
    74      48355
    Name: hotel_cluster, dtype: int64




```python
test.columns
```




    Index([u'id', u'date_time', u'site_name', u'posa_continent',
           u'user_location_country', u'user_location_region',
           u'user_location_city', u'orig_destination_distance', u'user_id',
           u'is_mobile', u'is_package', u'channel', u'srch_ci', u'srch_co',
           u'srch_adults_cnt', u'srch_children_cnt', u'srch_rm_cnt',
           u'srch_destination_id', u'srch_destination_type_id', u'hotel_continent',
           u'hotel_country', u'hotel_market'],
          dtype='object')




```python
train.dtypes
```




    date_time                     object
    site_name                      int64
    posa_continent                 int64
    user_location_country          int64
    user_location_region           int64
    user_location_city             int64
    orig_destination_distance    float64
    user_id                        int64
    is_mobile                      int64
    is_package                     int64
    channel                        int64
    srch_ci                       object
    srch_co                       object
    srch_adults_cnt                int64
    srch_children_cnt              int64
    srch_rm_cnt                    int64
    srch_destination_id            int64
    srch_destination_type_id       int64
    is_booking                     int64
    cnt                            int64
    hotel_continent                int64
    hotel_country                  int64
    hotel_market                   int64
    hotel_cluster                  int64
    dtype: object




```python
test.dtypes
```




    id                             int64
    date_time                     object
    site_name                      int64
    posa_continent                 int64
    user_location_country          int64
    user_location_region           int64
    user_location_city             int64
    orig_destination_distance    float64
    user_id                        int64
    is_mobile                      int64
    is_package                     int64
    channel                        int64
    srch_ci                       object
    srch_co                       object
    srch_adults_cnt                int64
    srch_children_cnt              int64
    srch_rm_cnt                    int64
    srch_destination_id            int64
    srch_destination_type_id       int64
    hotel_continent                int64
    hotel_country                  int64
    hotel_market                   int64
    dtype: object




```python
test_ids = set(test.user_id.unique())
```


```python
train_ids = set(train.user_id.unique())
```


```python
intersection_count = len(test_ids & train_ids)
```


```python
intersection_count == len(test_ids)
```




    True




```python
train["date_time"] = pd.to_datetime(train["date_time"])
```


```python
train["date_time"].head()
```




    0   2014-08-11 07:46:59
    1   2014-08-11 08:22:12
    2   2014-08-11 08:24:33
    3   2014-08-09 18:05:16
    4   2014-08-09 18:08:18
    Name: date_time, dtype: datetime64[ns]




```python
train["year"] = train["date_time"].dt.year
```


```python
train["month"] = train["date_time"].dt.month
```


```python
import random

unique_users = train.user_id.unique()
```


```python
sel_user_ids = [unique_users[i] for i in sorted(random.sample(range(len(unique_users)), 10000))]
sel_train = train[train.user_id.isin(sel_user_ids)]

```


```python
t1 = sel_train[((sel_train.year == 2013) | ((sel_train.year == 2014) & (sel_train.month < 8)))]
t2 = sel_train[((sel_train.year == 2014) & (sel_train.month >= 8))]
```


```python
t1.shape
```




    (198218, 26)




```python
t2.shape
```




    (115636, 27)




```python
len(sel_user_ids)
```




    10000




```python
t2 = t2[t2.is_booking == True]
```


```python
most_common_clusters = list(train.hotel_cluster.value_counts().head().index)
```


```python
train.hotel_cluster.value_counts().head(10)
```




    91    1043720
    41     772743
    48     754033
    64     704734
    65     670960
    5      620194
    98     589178
    59     570291
    42     551605
    21     550092
    Name: hotel_cluster, dtype: int64




```python
train.hotel_cluster.value_counts().head(10).index
```




    Int64Index([91, 41, 48, 64, 65, 5, 98, 59, 42, 21], dtype='int64')




```python
predictions = [most_common_clusters for i in range(t2.shape[0])]
```


```python
import ml_metrics as metrics
target = [[l] for l in t2["hotel_cluster"]]
metrics.mapk(target, predictions, k = 5)
```




    0.066330720418066424




```python
train.corr()["hotel_cluster"]
```




    site_name                   -0.022408
    posa_continent               0.014938
    user_location_country       -0.010477
    user_location_region         0.007453
    user_location_city           0.000831
    orig_destination_distance    0.007260
    user_id                      0.001052
    is_mobile                    0.008412
    is_package                   0.038733
    channel                      0.000707
    srch_adults_cnt              0.012309
    srch_children_cnt            0.016261
    srch_rm_cnt                 -0.005954
    srch_destination_id         -0.011712
    srch_destination_type_id    -0.032850
    is_booking                  -0.021548
    cnt                          0.002944
    hotel_continent             -0.013963
    hotel_country               -0.024289
    hotel_market                 0.034205
    hotel_cluster                1.000000
    year                        -0.001050
    month                       -0.000560
    Name: hotel_cluster, dtype: float64




```python
destinations.shape
```




    (62106, 150)




```python
destinations.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>srch_destination_id</th>
      <th>d1</th>
      <th>d2</th>
      <th>d3</th>
      <th>d4</th>
      <th>d5</th>
      <th>d6</th>
      <th>d7</th>
      <th>d8</th>
      <th>d9</th>
      <th>...</th>
      <th>d140</th>
      <th>d141</th>
      <th>d142</th>
      <th>d143</th>
      <th>d144</th>
      <th>d145</th>
      <th>d146</th>
      <th>d147</th>
      <th>d148</th>
      <th>d149</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>-2.198657</td>
      <td>-2.198657</td>
      <td>-2.198657</td>
      <td>-2.198657</td>
      <td>-2.198657</td>
      <td>-1.897627</td>
      <td>-2.198657</td>
      <td>-2.198657</td>
      <td>-1.897627</td>
      <td>...</td>
      <td>-2.198657</td>
      <td>-2.198657</td>
      <td>-2.198657</td>
      <td>-2.198657</td>
      <td>-2.198657</td>
      <td>-2.198657</td>
      <td>-2.198657</td>
      <td>-2.198657</td>
      <td>-2.198657</td>
      <td>-2.198657</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>-2.181690</td>
      <td>-2.181690</td>
      <td>-2.181690</td>
      <td>-2.082564</td>
      <td>-2.181690</td>
      <td>-2.165028</td>
      <td>-2.181690</td>
      <td>-2.181690</td>
      <td>-2.031597</td>
      <td>...</td>
      <td>-2.165028</td>
      <td>-2.181690</td>
      <td>-2.165028</td>
      <td>-2.181690</td>
      <td>-2.181690</td>
      <td>-2.165028</td>
      <td>-2.181690</td>
      <td>-2.181690</td>
      <td>-2.181690</td>
      <td>-2.181690</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>-2.183490</td>
      <td>-2.224164</td>
      <td>-2.224164</td>
      <td>-2.189562</td>
      <td>-2.105819</td>
      <td>-2.075407</td>
      <td>-2.224164</td>
      <td>-2.118483</td>
      <td>-2.140393</td>
      <td>...</td>
      <td>-2.224164</td>
      <td>-2.224164</td>
      <td>-2.196379</td>
      <td>-2.224164</td>
      <td>-2.192009</td>
      <td>-2.224164</td>
      <td>-2.224164</td>
      <td>-2.224164</td>
      <td>-2.224164</td>
      <td>-2.057548</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>-2.177409</td>
      <td>-2.177409</td>
      <td>-2.177409</td>
      <td>-2.177409</td>
      <td>-2.177409</td>
      <td>-2.115485</td>
      <td>-2.177409</td>
      <td>-2.177409</td>
      <td>-2.177409</td>
      <td>...</td>
      <td>-2.161081</td>
      <td>-2.177409</td>
      <td>-2.177409</td>
      <td>-2.177409</td>
      <td>-2.177409</td>
      <td>-2.177409</td>
      <td>-2.177409</td>
      <td>-2.177409</td>
      <td>-2.177409</td>
      <td>-2.177409</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>-2.189562</td>
      <td>-2.187783</td>
      <td>-2.194008</td>
      <td>-2.171153</td>
      <td>-2.152303</td>
      <td>-2.056618</td>
      <td>-2.194008</td>
      <td>-2.194008</td>
      <td>-2.145911</td>
      <td>...</td>
      <td>-2.187356</td>
      <td>-2.194008</td>
      <td>-2.191779</td>
      <td>-2.194008</td>
      <td>-2.194008</td>
      <td>-2.185161</td>
      <td>-2.194008</td>
      <td>-2.194008</td>
      <td>-2.194008</td>
      <td>-2.188037</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 150 columns</p>
</div>




```python
x = ["d{0}".format(i + 1) for i in range(149)]
```


```python

```


```python
from sklearn.decomposition import PCA

pca = PCA(n_components = 3)
dest_small = pca.fit_transform(destinations[["d{0}".format(i + 1) for i in range(149)]])
dest_small = pd.DataFrame(dest_small)
dest_small["srch_destination_id"] = destinations["srch_destination_id"]
```

    /Users/uyen/.local/lib/python2.7/site-packages/sklearn/utils/extmath.py:368: UserWarning: The number of power iterations is increased to 7 to achieve higher precision.
      warnings.warn("The number of power iterations is increased to "



```python
dest_small.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>srch_destination_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.044268</td>
      <td>0.169419</td>
      <td>0.032523</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.440761</td>
      <td>0.077405</td>
      <td>-0.091572</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.001033</td>
      <td>0.020677</td>
      <td>0.012108</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.480467</td>
      <td>-0.040345</td>
      <td>-0.019320</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.207253</td>
      <td>-0.042694</td>
      <td>-0.011744</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
def cal_fast_features(df):
    df["date_time"] = pd.to_datetime(df["date_time"])
    df["srch_ci"] = pd.to_datetime(df["srch_ci"], format = '%Y-%md-%d', errors = "coerce")
    df["srch_co"] = pd.to_datetime(df["srch_co"], format = '%Y-%m-%d', errors = "coerce")
    
    props = {}
    for prop in ["month", "day", "hour", "minute", "dayofweek", "quarter"]:
        props[prop] = getattr(df["date_time"].dt, prop)
        
    carryover = [p for p in df.columns if p not in ["date_time", "srch_ci", "srch_co"]]
    for prop in carryover:
        props[prop] = df[prop]
    
    date_props = ["month", "day", "dayofweek", "quarter"]
    
    for prop in date_props:
        props["ci_{0}".format(prop)] = getattr(df["srch_ci"].dt, prop)
        props["co_{0}".format(prop)] = getattr(df["srch_co"].dt, prop)
    
    props["stay_span"] = (df["srch_co"] - df["srch_ci"]).astype('timedelta64[h]')
    
    ret = pd.DataFrame(props)
    
    ret = ret.join(dest_small, on = "srch_destination_id", how = "left", rsuffix = "dest")
    ret = ret.drop("srch_destination_iddest", axis = 1)
    
    return ret

df = cal_fast_features(t1)
df.fillna(-1, inplace = True)
