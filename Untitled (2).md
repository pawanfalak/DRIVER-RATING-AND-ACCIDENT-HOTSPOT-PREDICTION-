

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
#import seaborn as sns
%matplotlib inline
from math import sin, cos, sqrt, atan2, radians
import warnings
warnings.filterwarnings('ignore')
```


```python
devc = 864504031502210
latitude1= 12.987503
longtitude1 = 77.740051 
place = 'Hudi' 
alarmtype = 'Overspeed'
speed = 32
timestamp= '2018-02-01T01:48:59.000Z'
tup=[devc,latitude1,longtitude1,place,alarmtype,speed,timestamp]

```


```python
rx=df=pd.read_csv('bangalore-cas-alerts.csv')
```


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 207617 entries, 0 to 207616
    Data columns (total 7 columns):
    deviceCode_deviceCode                 207617 non-null int64
    deviceCode_location_latitude          207617 non-null float64
    deviceCode_location_longitude         207617 non-null float64
    deviceCode_location_wardName          207617 non-null object
    deviceCode_pyld_alarmType             207617 non-null object
    deviceCode_pyld_speed                 207617 non-null int64
    deviceCode_time_recordedTime_$date    207617 non-null object
    dtypes: float64(2), int64(2), object(3)
    memory usage: 8.7+ MB
    


```python
df.drop_duplicates(subset=None, inplace=True)
```


```python
df.info()

```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 152276 entries, 0 to 207616
    Data columns (total 7 columns):
    deviceCode_deviceCode                 152276 non-null int64
    deviceCode_location_latitude          152276 non-null float64
    deviceCode_location_longitude         152276 non-null float64
    deviceCode_location_wardName          152276 non-null object
    deviceCode_pyld_alarmType             152276 non-null object
    deviceCode_pyld_speed                 152276 non-null int64
    deviceCode_time_recordedTime_$date    152276 non-null object
    dtypes: float64(2), int64(2), object(3)
    memory usage: 7.6+ MB
    


```python
df.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>deviceCode_deviceCode</th>
      <th>deviceCode_location_latitude</th>
      <th>deviceCode_location_longitude</th>
      <th>deviceCode_location_wardName</th>
      <th>deviceCode_pyld_alarmType</th>
      <th>deviceCode_pyld_speed</th>
      <th>deviceCode_time_recordedTime_$date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>864504031502210</td>
      <td>12.984595</td>
      <td>77.744087</td>
      <td>Kadugodi</td>
      <td>PCW</td>
      <td>32</td>
      <td>2018-02-01T01:48:59.000Z</td>
    </tr>
    <tr>
      <th>2</th>
      <td>864504031502210</td>
      <td>12.987233</td>
      <td>77.741119</td>
      <td>Garudachar Playa</td>
      <td>FCW</td>
      <td>41</td>
      <td>2018-02-01T01:50:00.000Z</td>
    </tr>
    <tr>
      <th>4</th>
      <td>864504031502210</td>
      <td>12.987503</td>
      <td>77.740051</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>37</td>
      <td>2018-02-01T01:50:11.000Z</td>
    </tr>
    <tr>
      <th>6</th>
      <td>864504031502210</td>
      <td>12.987523</td>
      <td>77.736702</td>
      <td>Kadugodi</td>
      <td>HMW</td>
      <td>32</td>
      <td>2018-02-01T01:50:50.000Z</td>
    </tr>
    <tr>
      <th>8</th>
      <td>864504031502210</td>
      <td>12.988210</td>
      <td>77.731369</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>27</td>
      <td>2018-02-01T01:52:26.000Z</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.to_csv('Banglore.csv')
```


```python
df=pd.read_csv('Banglore.csv')
```


```python
df.info()

```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 152276 entries, 0 to 152275
    Data columns (total 8 columns):
    Unnamed: 0                            152276 non-null int64
    deviceCode_deviceCode                 152276 non-null int64
    deviceCode_location_latitude          152276 non-null float64
    deviceCode_location_longitude         152276 non-null float64
    deviceCode_location_wardName          152276 non-null object
    deviceCode_pyld_alarmType             152276 non-null object
    deviceCode_pyld_speed                 152276 non-null int64
    deviceCode_time_recordedTime_$date    152276 non-null object
    dtypes: float64(2), int64(3), object(3)
    memory usage: 7.6+ MB
    


```python
df.drop('deviceCode_time_recordedTime_$date',axis=1,inplace=True)
```


```python
alarm=pd.get_dummies(df['deviceCode_pyld_alarmType'])
```


```python
df=pd.concat([df,alarm],axis=1)
```


```python
df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>deviceCode_deviceCode</th>
      <th>deviceCode_location_latitude</th>
      <th>deviceCode_location_longitude</th>
      <th>deviceCode_pyld_speed</th>
      <th>FCW</th>
      <th>HMW</th>
      <th>LDWL</th>
      <th>LDWR</th>
      <th>Overspeed</th>
      <th>PCW</th>
      <th>UFCW</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>152276.000000</td>
      <td>1.522760e+05</td>
      <td>152276.000000</td>
      <td>152276.000000</td>
      <td>152276.000000</td>
      <td>152276.000000</td>
      <td>152276.000000</td>
      <td>152276.000000</td>
      <td>152276.000000</td>
      <td>152276.000000</td>
      <td>152276.000000</td>
      <td>152276.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>94442.776807</td>
      <td>8.641311e+14</td>
      <td>12.970746</td>
      <td>77.721700</td>
      <td>22.144777</td>
      <td>0.169383</td>
      <td>0.171688</td>
      <td>0.006757</td>
      <td>0.005786</td>
      <td>0.130493</td>
      <td>0.116492</td>
      <td>0.399400</td>
    </tr>
    <tr>
      <th>std</th>
      <td>58963.179807</td>
      <td>2.963658e+11</td>
      <td>0.026638</td>
      <td>0.029724</td>
      <td>13.712247</td>
      <td>0.375091</td>
      <td>0.377110</td>
      <td>0.081926</td>
      <td>0.075843</td>
      <td>0.336846</td>
      <td>0.320816</td>
      <td>0.489777</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>8.620100e+14</td>
      <td>12.686663</td>
      <td>77.508179</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>45446.750000</td>
      <td>8.639770e+14</td>
      <td>12.956510</td>
      <td>77.706879</td>
      <td>11.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>83677.500000</td>
      <td>8.639770e+14</td>
      <td>12.973103</td>
      <td>77.727402</td>
      <td>22.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>142808.500000</td>
      <td>8.645040e+14</td>
      <td>12.987735</td>
      <td>77.743698</td>
      <td>32.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>207616.000000</td>
      <td>8.645040e+14</td>
      <td>13.070075</td>
      <td>77.806824</td>
      <td>83.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
#df.drop('deviceCode_pyld_alarmType',axis=1,inplace=True)
```


```python
df.drop('Unnamed: 0',axis=1,inplace=True)
```


```python
df.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>deviceCode_deviceCode</th>
      <th>deviceCode_location_latitude</th>
      <th>deviceCode_location_longitude</th>
      <th>deviceCode_location_wardName</th>
      <th>deviceCode_pyld_alarmType</th>
      <th>deviceCode_pyld_speed</th>
      <th>FCW</th>
      <th>HMW</th>
      <th>LDWL</th>
      <th>LDWR</th>
      <th>Overspeed</th>
      <th>PCW</th>
      <th>UFCW</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>864504031502210</td>
      <td>12.984595</td>
      <td>77.744087</td>
      <td>Kadugodi</td>
      <td>PCW</td>
      <td>32</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>864504031502210</td>
      <td>12.987233</td>
      <td>77.741119</td>
      <td>Garudachar Playa</td>
      <td>FCW</td>
      <td>41</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>864504031502210</td>
      <td>12.987503</td>
      <td>77.740051</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>37</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>864504031502210</td>
      <td>12.987523</td>
      <td>77.736702</td>
      <td>Kadugodi</td>
      <td>HMW</td>
      <td>32</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>864504031502210</td>
      <td>12.988210</td>
      <td>77.731369</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>27</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['deviceCode_location_wardName'].groupby(df['deviceCode_location_wardName']).count()
```




    deviceCode_location_wardName
    A Narayanapura              1321
    Agaram                        42
    BTM Layout                    15
    Banasavadi                   104
    Basavanapura                 464
    Bellanduru                  8551
    Benniganahalli                90
    Bharathi Nagar                 5
    C V Raman Nagar              439
    Chickpete                      9
    Devasandra                  1218
    Dharmaraya Swamy Temple        7
    Dodda Nekkundi             11063
    Domlur                       421
    Garudachar Playa            5866
    Gurappanapalya                 4
    HAL Airport                 2255
    HSR Layout                   120
    Hagadur                    16255
    Halsoor                       17
    Hemmigepura                   27
    Horamavu                     240
    Hoysala Nagar                220
    Hudi                       11276
    J P Nagar                     11
    Jaraganahalli                  5
    Jayanagar East                 3
    Jeevanbhima Nagar             67
    Jogupalya                     70
    K R Puram                    140
    Kacharkanahalli               56
    Kadugodi                   15448
    Kammanahalli                   3
    Konena Agrahara             1006
    Madivala                      11
    Marathahalli                2125
    New Tippasandara             375
    Other                       3626
    Ramamurthy Nagar             107
    Sampangiram Nagar             38
    Sarakki                       16
    Shantala Nagar                95
    Singasandra                   96
    Sudham Nagara                  1
    Varthuru                    4118
    Vasanthpura                   19
    Vijnana Nagar                490
    Vijnanapura                   40
    Yelchenahalli                  1
    other                      64280
    Name: deviceCode_location_wardName, dtype: int64




```python
#defining car place and location at any instant
place='Hudi'
loc=[latitude1,longtitude1]
```


```python
df1=df[df['deviceCode_location_wardName']==place]
```


```python
#np.sum(df1['HMW']==True)
```


```python
#define empty series for distance calculation
Distance = pd.Series([])
```


```python
#Functionn to calculate distance between the points
def function_(lat,long):
    # approximate radius of earth in km
    R = 6373.0

    lat1 = radians(loc[0])
    lon1 = radians(loc[1])
    lat2 = radians(lat)
    lon2 = radians(long)

    dlon = lon2 - lon1
    dlat = lat2 - lat1

    a = sin(dlat / 2)**2 + cos(lat1) * cos(lat2) * sin(dlon / 2)**2
    c = 2 * atan2(sqrt(a), sqrt(1 - a))

    distance = R * c
    return distance

```


```python
i=0
for index, row in df1.iterrows():
    y=function_(df1['deviceCode_location_latitude'].iloc[i],df1['deviceCode_location_longitude'].iloc[i])
    Distance.set_value(index,value=y)
    i=i+1

```


```python
Distance[2]
```




    2.9774868539355067e-05




```python
df1=pd.concat([df1,Distance],axis=1)
```


```python
df1.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>deviceCode_deviceCode</th>
      <th>deviceCode_location_latitude</th>
      <th>deviceCode_location_longitude</th>
      <th>deviceCode_location_wardName</th>
      <th>deviceCode_pyld_alarmType</th>
      <th>deviceCode_pyld_speed</th>
      <th>FCW</th>
      <th>HMW</th>
      <th>LDWL</th>
      <th>LDWR</th>
      <th>Overspeed</th>
      <th>PCW</th>
      <th>UFCW</th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>864504031502210</td>
      <td>12.987503</td>
      <td>77.740051</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>37</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.000030</td>
    </tr>
    <tr>
      <th>4</th>
      <td>864504031502210</td>
      <td>12.988210</td>
      <td>77.731369</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>27</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.944268</td>
    </tr>
    <tr>
      <th>5</th>
      <td>864504031502210</td>
      <td>12.988226</td>
      <td>77.731293</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>29</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.952659</td>
    </tr>
    <tr>
      <th>6</th>
      <td>864504031502210</td>
      <td>12.991210</td>
      <td>77.727478</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>14</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1.423720</td>
    </tr>
    <tr>
      <th>7</th>
      <td>864504031502210</td>
      <td>12.991193</td>
      <td>77.727829</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>12</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1.386790</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.sort_values(0,inplace=True)
```


```python
df1.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>deviceCode_deviceCode</th>
      <th>deviceCode_location_latitude</th>
      <th>deviceCode_location_longitude</th>
      <th>deviceCode_location_wardName</th>
      <th>deviceCode_pyld_alarmType</th>
      <th>deviceCode_pyld_speed</th>
      <th>FCW</th>
      <th>HMW</th>
      <th>LDWL</th>
      <th>LDWR</th>
      <th>Overspeed</th>
      <th>PCW</th>
      <th>UFCW</th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>864504031502210</td>
      <td>12.987503</td>
      <td>77.740051</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>37</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.000030</td>
    </tr>
    <tr>
      <th>25848</th>
      <td>864504031819929</td>
      <td>12.987491</td>
      <td>77.740051</td>
      <td>Hudi</td>
      <td>FCW</td>
      <td>30</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.001374</td>
    </tr>
    <tr>
      <th>64081</th>
      <td>864504031502210</td>
      <td>12.987491</td>
      <td>77.740067</td>
      <td>Hudi</td>
      <td>FCW</td>
      <td>30</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.002172</td>
    </tr>
    <tr>
      <th>1019</th>
      <td>864504031502210</td>
      <td>12.987496</td>
      <td>77.740021</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>38</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.003360</td>
    </tr>
    <tr>
      <th>273</th>
      <td>864504031502210</td>
      <td>12.987490</td>
      <td>77.740013</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>34</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.004364</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2 = df1.loc[df1[0]<0.5 , ['FCW', 'HMW', 'LDWL' ,'LDWR','Overspeed','PCW','UFCW']]
```


```python
df2.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FCW</th>
      <th>HMW</th>
      <th>LDWL</th>
      <th>LDWR</th>
      <th>Overspeed</th>
      <th>PCW</th>
      <th>UFCW</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>25848</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>64081</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1019</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>273</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
list1=['FCW', 'HMW', 'LDWL' ,'LDWR','Overspeed','PCW','UFCW']
```


```python
def countval(list1,Df2,j):
    x=np.sum(Df2[list1[j]]==1)
    y=(Df2[list1[j]].count())-x
    return [x,y]
```


```python
z=[]
```


```python
for i in range(0,len(list1)):
    z.append(countval(list1,df2,i))
```


```python
z
```




    [[87, 436], [141, 382], [4, 519], [0, 523], [98, 425], [18, 505], [175, 348]]




```python
df_ = pd.DataFrame(data=z,columns=['True','False'],index=['FCW', 'HMW', 'LDWL' ,'LDWR','Overspeed','PCW','UFCW'])
#df_ = df_.fillna(0) # with 0s rather than NaNs
```


```python
df_
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>True</th>
      <th>False</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>FCW</th>
      <td>87</td>
      <td>436</td>
    </tr>
    <tr>
      <th>HMW</th>
      <td>141</td>
      <td>382</td>
    </tr>
    <tr>
      <th>LDWL</th>
      <td>4</td>
      <td>519</td>
    </tr>
    <tr>
      <th>LDWR</th>
      <td>0</td>
      <td>523</td>
    </tr>
    <tr>
      <th>Overspeed</th>
      <td>98</td>
      <td>425</td>
    </tr>
    <tr>
      <th>PCW</th>
      <td>18</td>
      <td>505</td>
    </tr>
    <tr>
      <th>UFCW</th>
      <td>175</td>
      <td>348</td>
    </tr>
  </tbody>
</table>
</div>




```python
t1=np.sum(df_['True'])
t2=np.sum(df_['False'])
```


```python
df_.loc['Total']=(t1,t2)
```


```python
df_
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>True</th>
      <th>False</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>FCW</th>
      <td>87</td>
      <td>436</td>
    </tr>
    <tr>
      <th>HMW</th>
      <td>141</td>
      <td>382</td>
    </tr>
    <tr>
      <th>LDWL</th>
      <td>4</td>
      <td>519</td>
    </tr>
    <tr>
      <th>LDWR</th>
      <td>0</td>
      <td>523</td>
    </tr>
    <tr>
      <th>Overspeed</th>
      <td>98</td>
      <td>425</td>
    </tr>
    <tr>
      <th>PCW</th>
      <td>18</td>
      <td>505</td>
    </tr>
    <tr>
      <th>UFCW</th>
      <td>175</td>
      <td>348</td>
    </tr>
    <tr>
      <th>Total</th>
      <td>523</td>
      <td>3138</td>
    </tr>
  </tbody>
</table>
</div>




```python
perc_probility = pd.Series([])
```


```python
def func1(tr,fa):
    return ((tr/(tr+fa))*100)
    
```


```python
j=0
for index, row in df_.iterrows():
    k=func1(df_['True'].iloc[j],df_['False'].iloc[j])
    perc_probility.set_value(index,value=k)
    j=j+1
    
```


```python
perc_probility
```




    FCW          16.634799
    HMW          26.959847
    LDWL          0.764818
    LDWR          0.000000
    Overspeed    18.738050
    PCW           3.441683
    UFCW         33.460803
    Total        14.285714
    dtype: float64




```python
df_=pd.concat([df_,perc_probility],axis=1)
```


```python
df_
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>True</th>
      <th>False</th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>FCW</th>
      <td>87</td>
      <td>436</td>
      <td>16.634799</td>
    </tr>
    <tr>
      <th>HMW</th>
      <td>141</td>
      <td>382</td>
      <td>26.959847</td>
    </tr>
    <tr>
      <th>LDWL</th>
      <td>4</td>
      <td>519</td>
      <td>0.764818</td>
    </tr>
    <tr>
      <th>LDWR</th>
      <td>0</td>
      <td>523</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Overspeed</th>
      <td>98</td>
      <td>425</td>
      <td>18.738050</td>
    </tr>
    <tr>
      <th>PCW</th>
      <td>18</td>
      <td>505</td>
      <td>3.441683</td>
    </tr>
    <tr>
      <th>UFCW</th>
      <td>175</td>
      <td>348</td>
      <td>33.460803</td>
    </tr>
    <tr>
      <th>Total</th>
      <td>523</td>
      <td>3138</td>
      <td>14.285714</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>deviceCode_deviceCode</th>
      <th>deviceCode_location_latitude</th>
      <th>deviceCode_location_longitude</th>
      <th>deviceCode_location_wardName</th>
      <th>deviceCode_pyld_alarmType</th>
      <th>deviceCode_pyld_speed</th>
      <th>FCW</th>
      <th>HMW</th>
      <th>LDWL</th>
      <th>LDWR</th>
      <th>Overspeed</th>
      <th>PCW</th>
      <th>UFCW</th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>864504031502210</td>
      <td>12.987503</td>
      <td>77.740051</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>37</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.000030</td>
    </tr>
    <tr>
      <th>25848</th>
      <td>864504031819929</td>
      <td>12.987491</td>
      <td>77.740051</td>
      <td>Hudi</td>
      <td>FCW</td>
      <td>30</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.001374</td>
    </tr>
    <tr>
      <th>64081</th>
      <td>864504031502210</td>
      <td>12.987491</td>
      <td>77.740067</td>
      <td>Hudi</td>
      <td>FCW</td>
      <td>30</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.002172</td>
    </tr>
    <tr>
      <th>1019</th>
      <td>864504031502210</td>
      <td>12.987496</td>
      <td>77.740021</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>38</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.003360</td>
    </tr>
    <tr>
      <th>273</th>
      <td>864504031502210</td>
      <td>12.987490</td>
      <td>77.740013</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>34</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.004364</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.columns=['deviceCode_deviceCode',  'deviceCode_location_latitude',
       'deviceCode_location_longitude',  'deviceCode_location_wardName',
           'deviceCode_pyld_alarmType',         'deviceCode_pyld_speed',
                                 'FCW',                           'HMW',
                                'LDWL',                          'LDWR',
                           'Overspeed',                           'PCW',
                                'UFCW',                               'Distance_from_given_location_in_Km']
```


```python
l1=[]
for i in range(0,11276):
    l1.append(0.0)
```


```python
df1['Probability'] = pd.Series(data=l1, index=df1.index)
```


```python
df1.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>deviceCode_deviceCode</th>
      <th>deviceCode_location_latitude</th>
      <th>deviceCode_location_longitude</th>
      <th>deviceCode_location_wardName</th>
      <th>deviceCode_pyld_alarmType</th>
      <th>deviceCode_pyld_speed</th>
      <th>FCW</th>
      <th>HMW</th>
      <th>LDWL</th>
      <th>LDWR</th>
      <th>Overspeed</th>
      <th>PCW</th>
      <th>UFCW</th>
      <th>Distance_from_given_location_in_Km</th>
      <th>Probability</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>864504031502210</td>
      <td>12.987503</td>
      <td>77.740051</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>37</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.000030</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>25848</th>
      <td>864504031819929</td>
      <td>12.987491</td>
      <td>77.740051</td>
      <td>Hudi</td>
      <td>FCW</td>
      <td>30</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.001374</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>64081</th>
      <td>864504031502210</td>
      <td>12.987491</td>
      <td>77.740067</td>
      <td>Hudi</td>
      <td>FCW</td>
      <td>30</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.002172</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1019</th>
      <td>864504031502210</td>
      <td>12.987496</td>
      <td>77.740021</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>38</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.003360</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>273</th>
      <td>864504031502210</td>
      <td>12.987490</td>
      <td>77.740013</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>34</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.004364</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_[0]['Overspeed']
```




    18.738049713193117




```python
j=0
for index, row in df1.iterrows():
        if df1['deviceCode_pyld_alarmType'].iloc[j]=='UFCW':
            df1['Probability'][df1.index[j]]=df_[0]['UFCW']
        elif df1['deviceCode_pyld_alarmType'].iloc[j]=='FCW':
            df1['Probability'][df1.index[j]]=df_[0]['FCW']
        elif df1['deviceCode_pyld_alarmType'].iloc[j]=='HMW':
            df1['Probability'][df1.index[j]]=df_[0]['HMW']
        elif df1['deviceCode_pyld_alarmType'].iloc[j]=='LDWL':
            df1['Probability'][df1.index[j]]=df_[0]['LDWL']
        elif df1['deviceCode_pyld_alarmType'].iloc[j]=='LDWR':
            df1['Probability'][df1.index[j]]=df_[0]['LDWR']
        elif df1['deviceCode_pyld_alarmType'].iloc[j]=='PCW':
            df1['Probability'][df1.index[j]]=df_[0]['PCW']
        elif df1['deviceCode_pyld_alarmType'].iloc[j]=='Overspeed':
            df1['Probability'][df1.index[j]]=df_[0]['Overspeed']
        j=j+1
        if j==5:
            break
```


```python
dfx=df1.head()
dfx
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>deviceCode_deviceCode</th>
      <th>deviceCode_location_latitude</th>
      <th>deviceCode_location_longitude</th>
      <th>deviceCode_location_wardName</th>
      <th>deviceCode_pyld_alarmType</th>
      <th>deviceCode_pyld_speed</th>
      <th>FCW</th>
      <th>HMW</th>
      <th>LDWL</th>
      <th>LDWR</th>
      <th>Overspeed</th>
      <th>PCW</th>
      <th>UFCW</th>
      <th>Distance_from_given_location_in_Km</th>
      <th>Probability</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>864504031502210</td>
      <td>12.987503</td>
      <td>77.740051</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>37</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.000030</td>
      <td>18.738050</td>
    </tr>
    <tr>
      <th>25848</th>
      <td>864504031819929</td>
      <td>12.987491</td>
      <td>77.740051</td>
      <td>Hudi</td>
      <td>FCW</td>
      <td>30</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.001374</td>
      <td>16.634799</td>
    </tr>
    <tr>
      <th>64081</th>
      <td>864504031502210</td>
      <td>12.987491</td>
      <td>77.740067</td>
      <td>Hudi</td>
      <td>FCW</td>
      <td>30</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0.002172</td>
      <td>16.634799</td>
    </tr>
    <tr>
      <th>1019</th>
      <td>864504031502210</td>
      <td>12.987496</td>
      <td>77.740021</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>38</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.003360</td>
      <td>18.738050</td>
    </tr>
    <tr>
      <th>273</th>
      <td>864504031502210</td>
      <td>12.987490</td>
      <td>77.740013</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>34</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0.004364</td>
      <td>18.738050</td>
    </tr>
  </tbody>
</table>
</div>




```python
rating=0
```


```python
x=dfx['Probability'].max()
```


```python
dfx[dfx['Probability']==x]['deviceCode_pyld_alarmType'].iloc[0]
df_[0][alarmtype]
```




    18.738049713193117




```python
ym=dfx['Distance_from_given_location_in_Km'].min()
```


```python
dfx[dfx['Distance_from_given_location_in_Km']==ym]['deviceCode_pyld_alarmType'].iloc[0]

```




    'Overspeed'




```python
if (dfx[dfx['Probability']==x]['deviceCode_pyld_alarmType'].iloc[0]==alarmtype) or (dfx[dfx['Distance_from_given_location_in_Km']==ym]['deviceCode_pyld_alarmType'].iloc[0]
==alarmtype):
        rating=1
elif (df_[0][alarmtype])>=0 and (df_[0][alarmtype])<=10:
        rating=5
elif (df_[0][alarmtype])>10 and (df_[0][alarmtype])<=20:
        rating=4
elif (df_[0][alarmtype])>20 and (df_[0][alarmtype])<=30:
        rating=3
elif (df_[0][alarmtype])>30 and (df_[0][alarmtype])<=40:
        rating=2
else:
        rating=1
```


```python
print(rating)
```

    1
    


```python
pq=rx.xs(0)
```


```python
pq[0]=tup[0]
pq[1]=tup[1]
pq[2]=tup[2]
pq[3]=tup[3]
pq[4]=tup[4]
pq[5]=tup[5]
pq[6]=tup[6]
```


```python
my=rx.append(pq,ignore_index=True)
```


```python
my.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>deviceCode_deviceCode</th>
      <th>deviceCode_location_latitude</th>
      <th>deviceCode_location_longitude</th>
      <th>deviceCode_location_wardName</th>
      <th>deviceCode_pyld_alarmType</th>
      <th>deviceCode_pyld_speed</th>
      <th>deviceCode_time_recordedTime_$date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>864504031502210</td>
      <td>12.984595</td>
      <td>77.744087</td>
      <td>Kadugodi</td>
      <td>PCW</td>
      <td>32</td>
      <td>2018-02-01T01:48:59.000Z</td>
    </tr>
    <tr>
      <th>1</th>
      <td>864504031502210</td>
      <td>12.987233</td>
      <td>77.741119</td>
      <td>Garudachar Playa</td>
      <td>FCW</td>
      <td>41</td>
      <td>2018-02-01T01:50:00.000Z</td>
    </tr>
    <tr>
      <th>2</th>
      <td>864504031502210</td>
      <td>12.987503</td>
      <td>77.740051</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>37</td>
      <td>2018-02-01T01:50:11.000Z</td>
    </tr>
    <tr>
      <th>3</th>
      <td>864504031502210</td>
      <td>12.987523</td>
      <td>77.736702</td>
      <td>Kadugodi</td>
      <td>HMW</td>
      <td>32</td>
      <td>2018-02-01T01:50:50.000Z</td>
    </tr>
    <tr>
      <th>4</th>
      <td>864504031502210</td>
      <td>12.988210</td>
      <td>77.731369</td>
      <td>Hudi</td>
      <td>Overspeed</td>
      <td>27</td>
      <td>2018-02-01T01:52:26.000Z</td>
    </tr>
  </tbody>
</table>
</div>




```python
my.to_csv('BangloreUpdated.csv')
```
