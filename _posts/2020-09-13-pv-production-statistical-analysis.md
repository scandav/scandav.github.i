---
layout: post
title: PV Production - Data Analysis
---

```python
import sqlite3
import pandas as pd

db_file = 'pv_db.db'
conn = sqlite3.connect(db_file)
query = 'SELECT * FROM pv_data;'

df_pv = pd.read_sql(query, conn, parse_dates={'created': '%Y-%m-%d %H:%M:%S'})
df_pv.drop(columns=['nrg', 'pwr_peak'], inplace=True)
df_pv
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
      <th>id</th>
      <th>created</th>
      <th>grid_voltage</th>
      <th>grid_current</th>
      <th>grid_power</th>
      <th>invert_temp</th>
      <th>booster_temp</th>
      <th>pwr_peak_td</th>
      <th>nrg_td</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2019-10-04 19:00:06.315083</td>
      <td>224.6</td>
      <td>0.0</td>
      <td>0</td>
      <td>30.8</td>
      <td>30.5</td>
      <td>573</td>
      <td>10903</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2019-10-04 19:10:06.099258</td>
      <td>223.6</td>
      <td>0.0</td>
      <td>0</td>
      <td>30.6</td>
      <td>30.0</td>
      <td>573</td>
      <td>10903</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2019-10-05 07:30:05.401174</td>
      <td>226.7</td>
      <td>0.1</td>
      <td>24</td>
      <td>20.2</td>
      <td>18.5</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2019-10-05 07:40:06.007266</td>
      <td>226.7</td>
      <td>0.0</td>
      <td>29</td>
      <td>21.2</td>
      <td>19.6</td>
      <td>32</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>2019-10-05 07:50:05.717804</td>
      <td>226.6</td>
      <td>0.0</td>
      <td>72</td>
      <td>22.0</td>
      <td>20.8</td>
      <td>70</td>
      <td>9</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>51768</th>
      <td>51769</td>
      <td>2020-09-12 19:40:09.038391</td>
      <td>225.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>37.9</td>
      <td>37.6</td>
      <td>2585</td>
      <td>18283</td>
    </tr>
    <tr>
      <th>51769</th>
      <td>51770</td>
      <td>2020-09-12 19:45:09.319136</td>
      <td>224.6</td>
      <td>0.0</td>
      <td>0</td>
      <td>37.8</td>
      <td>37.4</td>
      <td>2585</td>
      <td>18283</td>
    </tr>
    <tr>
      <th>51770</th>
      <td>51771</td>
      <td>2020-09-12 19:50:08.722243</td>
      <td>222.9</td>
      <td>0.0</td>
      <td>0</td>
      <td>37.6</td>
      <td>37.1</td>
      <td>2585</td>
      <td>18283</td>
    </tr>
    <tr>
      <th>51771</th>
      <td>51772</td>
      <td>2020-09-12 19:55:09.105575</td>
      <td>223.2</td>
      <td>0.0</td>
      <td>0</td>
      <td>37.5</td>
      <td>36.9</td>
      <td>2585</td>
      <td>18283</td>
    </tr>
    <tr>
      <th>51772</th>
      <td>51773</td>
      <td>2020-09-12 20:00:09.579805</td>
      <td>224.6</td>
      <td>0.0</td>
      <td>0</td>
      <td>37.4</td>
      <td>36.8</td>
      <td>2585</td>
      <td>18283</td>
    </tr>
  </tbody>
</table>
<p>51773 rows × 9 columns</p>
</div>




```python
df_pv.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 51773 entries, 0 to 51772
    Data columns (total 9 columns):
     #   Column        Non-Null Count  Dtype         
    ---  ------        --------------  -----         
     0   id            51773 non-null  int64         
     1   created       51773 non-null  datetime64[ns]
     2   grid_voltage  51773 non-null  float64       
     3   grid_current  51773 non-null  float64       
     4   grid_power    51773 non-null  int64         
     5   invert_temp   51773 non-null  float64       
     6   booster_temp  51773 non-null  float64       
     7   pwr_peak_td   51773 non-null  int64         
     8   nrg_td        51773 non-null  int64         
    dtypes: datetime64[ns](1), float64(4), int64(4)
    memory usage: 3.6 MB



```python
df_pv.describe()
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
      <th>id</th>
      <th>grid_voltage</th>
      <th>grid_current</th>
      <th>grid_power</th>
      <th>invert_temp</th>
      <th>booster_temp</th>
      <th>pwr_peak_td</th>
      <th>nrg_td</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>51773.00000</td>
      <td>51773.000000</td>
      <td>51773.000000</td>
      <td>51773.000000</td>
      <td>51773.000000</td>
      <td>51773.000000</td>
      <td>51773.000000</td>
      <td>51773.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>25887.00000</td>
      <td>228.872273</td>
      <td>4.475850</td>
      <td>1080.030035</td>
      <td>33.875379</td>
      <td>33.579854</td>
      <td>2086.641010</td>
      <td>8029.108802</td>
    </tr>
    <tr>
      <th>std</th>
      <td>14945.72208</td>
      <td>7.486592</td>
      <td>4.323384</td>
      <td>1012.921134</td>
      <td>9.836976</td>
      <td>9.553740</td>
      <td>1324.451999</td>
      <td>7971.534152</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.00000</td>
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
      <td>12944.00000</td>
      <td>226.500000</td>
      <td>0.500000</td>
      <td>169.000000</td>
      <td>25.500000</td>
      <td>25.800000</td>
      <td>981.000000</td>
      <td>1072.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>25887.00000</td>
      <td>228.700000</td>
      <td>3.200000</td>
      <td>791.000000</td>
      <td>33.400000</td>
      <td>33.400000</td>
      <td>2109.000000</td>
      <td>5189.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>38830.00000</td>
      <td>231.500000</td>
      <td>7.500000</td>
      <td>1780.000000</td>
      <td>42.000000</td>
      <td>41.600000</td>
      <td>3200.000000</td>
      <td>13616.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>51773.00000</td>
      <td>241.700000</td>
      <td>19.200000</td>
      <td>4670.000000</td>
      <td>55.000000</td>
      <td>52.900000</td>
      <td>5186.000000</td>
      <td>29325.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_pv_no_zeroV = df_pv[df_pv.grid_voltage != 0.0]
df_pv_no_zeroV.plot(x='created', y='grid_voltage')
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1246a6970>




![png](/assets/img/output_3_1.png)



```python
df_pv_no_zeroV['grid_voltage'].plot(kind='hist', bins=25, density=True)
df_pv_no_zeroV.describe()
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
      <th>id</th>
      <th>grid_voltage</th>
      <th>grid_current</th>
      <th>grid_power</th>
      <th>invert_temp</th>
      <th>booster_temp</th>
      <th>pwr_peak_td</th>
      <th>nrg_td</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>51731.000000</td>
      <td>51731.000000</td>
      <td>51731.000000</td>
      <td>51731.000000</td>
      <td>51731.000000</td>
      <td>51731.000000</td>
      <td>51731.000000</td>
      <td>51731.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>25891.114515</td>
      <td>229.058093</td>
      <td>4.479436</td>
      <td>1080.906903</td>
      <td>33.902882</td>
      <td>33.607118</td>
      <td>2088.335138</td>
      <td>8035.627573</td>
    </tr>
    <tr>
      <th>std</th>
      <td>14945.664740</td>
      <td>3.678349</td>
      <td>4.323303</td>
      <td>1012.864462</td>
      <td>9.793478</td>
      <td>9.509563</td>
      <td>1323.653788</td>
      <td>7971.484572</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>214.200000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>12948.500000</td>
      <td>226.500000</td>
      <td>0.500000</td>
      <td>170.000000</td>
      <td>25.500000</td>
      <td>25.800000</td>
      <td>988.000000</td>
      <td>1076.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>25893.000000</td>
      <td>228.700000</td>
      <td>3.300000</td>
      <td>791.000000</td>
      <td>33.400000</td>
      <td>33.400000</td>
      <td>2112.000000</td>
      <td>5199.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>38833.500000</td>
      <td>231.500000</td>
      <td>7.500000</td>
      <td>1781.500000</td>
      <td>42.000000</td>
      <td>41.600000</td>
      <td>3200.000000</td>
      <td>13617.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>51773.000000</td>
      <td>241.700000</td>
      <td>19.200000</td>
      <td>4670.000000</td>
      <td>55.000000</td>
      <td>52.900000</td>
      <td>5186.000000</td>
      <td>29325.000000</td>
    </tr>
  </tbody>
</table>
</div>




![png](/assets/img/output_4_1.png)



```python
df_pv_no_zeroV['invert_temp'].plot(kind='hist', density=True, bins=30, legend=True)
df_pv_no_zeroV['booster_temp'].plot(kind='hist', density=True, bins=30, alpha=0.75, legend=True)
```




    <matplotlib.axes._subplots.AxesSubplot at 0x1249d5f10>




![png](/assets/img/output_5_1.png)



```python
power_distribution = df_pv.groupby([df_pv.created.dt.hour])['grid_power'].sum()
power_distribution.plot()
power_distribution
```




    created
    5         757
    6      116910
    7      919106
    8     2515051
    9     4500315
    10    6119169
    11    7151284
    12    7571158
    13    7315763
    14    6373130
    15    5224561
    16    3808694
    17    2342670
    18    1301032
    19     570694
    20      85758
    21        343
    Name: grid_power, dtype: int64




![png](/assets/img/output_6_1.png)



```python
power_distribution_month = df_pv.groupby([df_pv.created.dt.month, df_pv.created.dt.hour])['grid_power'].sum()

import matplotlib.pyplot as plt

fig, ax = plt.subplots()

for i in [1, 4, 7, 10]:
    ax.plot(power_distribution_month[i], '.-')
```


![png](/assets/img/output_7_0.png)



```python
from pandas.plotting import scatter_matrix

scatter_matrix(df_pv_no_zeroV[['grid_voltage', 'grid_current', 'grid_power', 'invert_temp', 'booster_temp']], 
               alpha=0.2, figsize=(6, 6), diagonal='hist')
plt.show()
```


![png](/assets/img/output_8_0.png)

## Estimated Energy Production vs Produced

Let's try to compare the produced energy with the estimations computed based on irradiance. Here are some details of the PV system.

![PV Setup from Google Maps](/assets/img/pv_google_maps.png)

It is composed of two modules:

Detail       | East Module   |  West Module
------------ | ------------- | ------------
Solar Azimut [$\deg$] | -70 | 110
Panel Tilt [$\deg$]   | 18  | 18
No. Modules [-]       | 14  | 9
Nominal Power [$kW$]  | 3.5 | 2.25

Given the geo-location and the parameters reported above regarding panels inclination, one could retrieve the monthly-averaged daily global solar radiation $[kWh/m^2]$, from [ENEA](http://www.solaritaly.enea.it/CalcRggmmIncl/Calcola1.php).

Month       | East Module   |  West Module
------------ | ------------- | ------------
January | 1,75	| 1,31
February | 2,61	| 2,13
March | 3,89	| 3,4
April | 4,76	| 4,43
May | 5,43	| 5,26
June | 6	| 5,91
July | 6,06	| 5,93
August | 5,24	| 4,98
September | 4,08	| 3,7
October | 2,82	| 2,4
November | 1,86	| 1,46
December | 1,38	| 1,03

Knowing geo-location, the Temperature Correction Factor is retrieved from the panels' datasheet. It takes into account the diffence in effeciency due to temperature with respect to the 25 degrees C condition. Below is a summar of what discussed so far.


```python
df_radiation = pd.read_excel('fotovoltaico_casa.xlsx', sheet_name='Modules')

from datetime import date
days_in_month = [(date(2020, i+1, 1) - date(2020, i, 1)).days for i in range(1, 12)] + [31]
days_in_month[1] -= 0.75 # February has 28.5 days

df_radiation['Days'] = days_in_month * 2
df_radiation.head()
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
      <th>Module</th>
      <th>Month</th>
      <th>GlobalRad</th>
      <th>TCF</th>
      <th>Days</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>East</td>
      <td>1</td>
      <td>1.75</td>
      <td>1.02</td>
      <td>31.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>East</td>
      <td>2</td>
      <td>2.61</td>
      <td>1.01</td>
      <td>28.25</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East</td>
      <td>3</td>
      <td>3.89</td>
      <td>0.95</td>
      <td>31.00</td>
    </tr>
    <tr>
      <th>3</th>
      <td>East</td>
      <td>4</td>
      <td>4.76</td>
      <td>0.91</td>
      <td>30.00</td>
    </tr>
    <tr>
      <th>4</th>
      <td>East</td>
      <td>5</td>
      <td>5.43</td>
      <td>0.88</td>
      <td>31.00</td>
    </tr>
  </tbody>
</table>
</div>



The estimated energy production can now be computed. Let us first start with the equivalent hours of peak production for each month:


```python
df_radiation['Heq'] = df_radiation['GlobalRad'] * df_radiation['TCF'] * df_radiation['Days']
```

Assuming a loss coefficient of 0.8 for the system - including inverter and grid efficiencies - the total energy produced [$kWh$] can be computed:


```python
df_radiation.loc[df_radiation['Module'] == 'East', 'PPeak'] = 3.5
df_radiation.loc[df_radiation['Module'] == 'West', 'PPeak'] = 2.25

efficiency = 0.9925**8
df_radiation['Energy'] = df_radiation['PPeak'] * df_radiation['Heq'] * 0.8 * efficiency

print('Expected yearly production: {:.0f} kWh'.format(df_radiation['Energy'].sum(), 0))
```

    Expected yearly production: 5325 kWh



```python
est_energy = df_radiation.groupby('Month')['Energy'].sum()
est_energy
```




    Month
    1     216.084170
    2     299.327834
    3     471.720550
    4     547.554246
    5     633.713335
    6     674.275039
    7     693.863003
    8     593.305330
    9     454.621409
    10    349.430586
    11    221.339949
    12    170.235504
    Name: Energy, dtype: float64




```python
df = df_pv_no_zeroV
daily_energy = df[df.created >= '2020-01-01'].groupby([df.created.dt.month, df.created.dt.day])['nrg_td'].max()
monthly_energy = daily_energy.groupby(level=[0]).sum() / 1000
monthly_energy
```




    created
    1    180.499
    2    269.901
    3    362.871
    4    585.782
    5    646.194
    6    657.542
    7    717.636
    8    593.234
    9    211.107
    Name: nrg_td, dtype: float64




```python
df1 = pd.DataFrame({'Expected': est_energy, 'Produced': monthly_energy})

#monthly_energy.cumsum().plot()
#est_energy.cumsum().plot()

#monthly_energy.join(est_energy).plot.bar()
#est_energy.plot.bar()
fig, ax = plt.subplots(2, 1, figsize=[12, 8])

df1.plot(kind='bar', ax=ax[0])
df1['Expected'].cumsum().plot(ax=ax[1])
df1['Produced'].cumsum().plot(ax=ax[1])
```




    <matplotlib.axes._subplots.AxesSubplot at 0x12445eca0>




![png](/assets/img/output_17_1.png)



```python

```
