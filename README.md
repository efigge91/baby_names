
#Observations

*Name popularity has fluctuated over time

*Names will hold top spots in popularity for a period of time and then diminish greatly

*In earlier years, the longevity of a name was greater -- that cycle has shortened

*Fewer male names have held top 3 spots in popularity than female names

*Regional impacts can be seen in name uniqueness

*Gender preference for names, in some cases, have shifted (names that were once more popular with males became more popular with females and vice versa)

*Popular culture (music, movie stars, sports figures, etc.) have shown to impact name selection


```python
import pandas as pd
import os
import matplotlib.pyplot as plt
import numpy as np
```


```python
data_file = os.path.join("NationalNames.csv")
national_names_df = pd.read_csv(data_file)
data_file = os.path.join("StateNames.csv")
state_names_df = pd.read_csv(data_file)
```


```python
national_names_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>Name</th>
      <th>Year</th>
      <th>Gender</th>
      <th>Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Mary</td>
      <td>1880</td>
      <td>F</td>
      <td>7065</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Anna</td>
      <td>1880</td>
      <td>F</td>
      <td>2604</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Emma</td>
      <td>1880</td>
      <td>F</td>
      <td>2003</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Elizabeth</td>
      <td>1880</td>
      <td>F</td>
      <td>1939</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Minnie</td>
      <td>1880</td>
      <td>F</td>
      <td>1746</td>
    </tr>
  </tbody>
</table>
</div>




```python
state_names_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>Name</th>
      <th>Year</th>
      <th>Gender</th>
      <th>State</th>
      <th>Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Mary</td>
      <td>1910</td>
      <td>F</td>
      <td>AK</td>
      <td>14</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Annie</td>
      <td>1910</td>
      <td>F</td>
      <td>AK</td>
      <td>12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Anna</td>
      <td>1910</td>
      <td>F</td>
      <td>AK</td>
      <td>10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Margaret</td>
      <td>1910</td>
      <td>F</td>
      <td>AK</td>
      <td>8</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Helen</td>
      <td>1910</td>
      <td>F</td>
      <td>AK</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>




```python
national_names_male_df = national_names_df.loc[national_names_df["Gender"]=="M"]
national_names_female_df = national_names_df.loc[national_names_df["Gender"]=="F"]

national_names_female_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>Name</th>
      <th>Year</th>
      <th>Gender</th>
      <th>Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Mary</td>
      <td>1880</td>
      <td>F</td>
      <td>7065</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Anna</td>
      <td>1880</td>
      <td>F</td>
      <td>2604</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Emma</td>
      <td>1880</td>
      <td>F</td>
      <td>2003</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Elizabeth</td>
      <td>1880</td>
      <td>F</td>
      <td>1939</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Minnie</td>
      <td>1880</td>
      <td>F</td>
      <td>1746</td>
    </tr>
  </tbody>
</table>
</div>



##Add Ranking to the National and State Files
##Ranking will be within each Year (National)
##Ranking will be within each State, Each Year (State)


```python
national_names_male_df['Rank'] = national_names_male_df.groupby('Year')['Count'].rank(ascending=False, method="min").astype(int)
national_names_male_df.head()
```

    C:\Users\sboxberg\Anaconda3\lib\site-packages\ipykernel_launcher.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      """Entry point for launching an IPython kernel.
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>Name</th>
      <th>Year</th>
      <th>Gender</th>
      <th>Count</th>
      <th>Rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>942</th>
      <td>943</td>
      <td>John</td>
      <td>1880</td>
      <td>M</td>
      <td>9655</td>
      <td>1</td>
    </tr>
    <tr>
      <th>943</th>
      <td>944</td>
      <td>William</td>
      <td>1880</td>
      <td>M</td>
      <td>9532</td>
      <td>2</td>
    </tr>
    <tr>
      <th>944</th>
      <td>945</td>
      <td>James</td>
      <td>1880</td>
      <td>M</td>
      <td>5927</td>
      <td>3</td>
    </tr>
    <tr>
      <th>945</th>
      <td>946</td>
      <td>Charles</td>
      <td>1880</td>
      <td>M</td>
      <td>5348</td>
      <td>4</td>
    </tr>
    <tr>
      <th>946</th>
      <td>947</td>
      <td>George</td>
      <td>1880</td>
      <td>M</td>
      <td>5126</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
national_names_female_df['Rank'] = national_names_female_df.groupby('Year')['Count'].rank(ascending=False,method="min").astype(int)
national_names_female_df.head()
```

    C:\Users\sboxberg\Anaconda3\lib\site-packages\ipykernel_launcher.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      """Entry point for launching an IPython kernel.
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>Name</th>
      <th>Year</th>
      <th>Gender</th>
      <th>Count</th>
      <th>Rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Mary</td>
      <td>1880</td>
      <td>F</td>
      <td>7065</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Anna</td>
      <td>1880</td>
      <td>F</td>
      <td>2604</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Emma</td>
      <td>1880</td>
      <td>F</td>
      <td>2003</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Elizabeth</td>
      <td>1880</td>
      <td>F</td>
      <td>1939</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Minnie</td>
      <td>1880</td>
      <td>F</td>
      <td>1746</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
state_names_male_df = state_names_df.loc[state_names_df["Gender"]=="M"]
state_names_female_df = state_names_df.loc[state_names_df["Gender"]=="F"]
```


```python
state_names_male_df['Rank'] = state_names_male_df.groupby(['Year','State'])['Count'].rank(ascending=False, method="min").astype(int)
state_names_male_df.head()
```

    C:\Users\sboxberg\Anaconda3\lib\site-packages\ipykernel_launcher.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      """Entry point for launching an IPython kernel.
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>Name</th>
      <th>Year</th>
      <th>Gender</th>
      <th>State</th>
      <th>Count</th>
      <th>Rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>13753</th>
      <td>13754</td>
      <td>John</td>
      <td>1910</td>
      <td>M</td>
      <td>AK</td>
      <td>8</td>
      <td>1</td>
    </tr>
    <tr>
      <th>13754</th>
      <td>13755</td>
      <td>James</td>
      <td>1910</td>
      <td>M</td>
      <td>AK</td>
      <td>7</td>
      <td>2</td>
    </tr>
    <tr>
      <th>13755</th>
      <td>13756</td>
      <td>Paul</td>
      <td>1910</td>
      <td>M</td>
      <td>AK</td>
      <td>6</td>
      <td>3</td>
    </tr>
    <tr>
      <th>13756</th>
      <td>13757</td>
      <td>Robert</td>
      <td>1910</td>
      <td>M</td>
      <td>AK</td>
      <td>6</td>
      <td>3</td>
    </tr>
    <tr>
      <th>13757</th>
      <td>13758</td>
      <td>Carl</td>
      <td>1910</td>
      <td>M</td>
      <td>AK</td>
      <td>5</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>




```python
state_names_female_df['Rank'] = state_names_female_df.groupby(['Year','State'])['Count'].rank(ascending=False, method="min").astype(int)
state_names_female_df.head()
```

    C:\Users\sboxberg\Anaconda3\lib\site-packages\ipykernel_launcher.py:1: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      """Entry point for launching an IPython kernel.
    




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>Name</th>
      <th>Year</th>
      <th>Gender</th>
      <th>State</th>
      <th>Count</th>
      <th>Rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Mary</td>
      <td>1910</td>
      <td>F</td>
      <td>AK</td>
      <td>14</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Annie</td>
      <td>1910</td>
      <td>F</td>
      <td>AK</td>
      <td>12</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Anna</td>
      <td>1910</td>
      <td>F</td>
      <td>AK</td>
      <td>10</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Margaret</td>
      <td>1910</td>
      <td>F</td>
      <td>AK</td>
      <td>8</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Helen</td>
      <td>1910</td>
      <td>F</td>
      <td>AK</td>
      <td>7</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



##Determine the Year when a name first appeared and add to the master dataframe (Male & Female)


```python
first_occurence_male=national_names_male_df.groupby("Name").min()
```


```python
first_occurence_male.reset_index(inplace=True)
first_occurence_male.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Id</th>
      <th>Year</th>
      <th>Gender</th>
      <th>Count</th>
      <th>Rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aaban</td>
      <td>1585835</td>
      <td>2007</td>
      <td>M</td>
      <td>5</td>
      <td>5432</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aabid</td>
      <td>1452434</td>
      <td>2003</td>
      <td>M</td>
      <td>5</td>
      <td>10889</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aadam</td>
      <td>1022129</td>
      <td>1987</td>
      <td>M</td>
      <td>5</td>
      <td>4836</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aadan</td>
      <td>1452435</td>
      <td>2003</td>
      <td>M</td>
      <td>5</td>
      <td>4270</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aadarsh</td>
      <td>1360531</td>
      <td>2000</td>
      <td>M</td>
      <td>5</td>
      <td>5023</td>
    </tr>
  </tbody>
</table>
</div>




```python
first_occurence_male.drop(['Id','Gender','Count','Rank'], axis=1, inplace=True)
first_occurence_male.columns = ['Name', 'First Year']
first_occurence_male.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>First Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aaban</td>
      <td>2007</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aabid</td>
      <td>2003</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aadam</td>
      <td>1987</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aadan</td>
      <td>2003</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aadarsh</td>
      <td>2000</td>
    </tr>
  </tbody>
</table>
</div>




```python
first_occurence_female=national_names_female_df.groupby("Name").min()
```


```python
first_occurence_female.reset_index(inplace=True)
first_occurence_female.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Id</th>
      <th>Year</th>
      <th>Gender</th>
      <th>Count</th>
      <th>Rank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aabha</td>
      <td>1704950</td>
      <td>2011</td>
      <td>F</td>
      <td>5</td>
      <td>10846</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aabriella</td>
      <td>1605341</td>
      <td>2008</td>
      <td>F</td>
      <td>5</td>
      <td>16388</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aaden</td>
      <td>1640162</td>
      <td>2009</td>
      <td>F</td>
      <td>5</td>
      <td>17254</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aadhira</td>
      <td>1740424</td>
      <td>2012</td>
      <td>F</td>
      <td>6</td>
      <td>8423</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aadhya</td>
      <td>1563740</td>
      <td>2007</td>
      <td>F</td>
      <td>9</td>
      <td>1033</td>
    </tr>
  </tbody>
</table>
</div>




```python
first_occurence_female.drop(['Id','Gender','Count','Rank'], axis=1, inplace=True)
first_occurence_female.columns = ['Name', 'First Year']
first_occurence_female.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>First Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aabha</td>
      <td>2011</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aabriella</td>
      <td>2008</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aaden</td>
      <td>2009</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aadhira</td>
      <td>2012</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aadhya</td>
      <td>2007</td>
    </tr>
  </tbody>
</table>
</div>




```python
first_occurence_male.sort_values("First Year", inplace=True, ascending=False)

first_occurence_male.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>First Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>22089</th>
      <td>Kuyper</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>9636</th>
      <td>Dhyaan</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>27552</th>
      <td>Nivin</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>18357</th>
      <td>Joesiyah</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>32247</th>
      <td>Semyon</td>
      <td>2014</td>
    </tr>
  </tbody>
</table>
</div>




```python
first_occurence_female.sort_values("First Year", inplace=True, ascending=False)
first_occurence_female.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>First Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4332</th>
      <td>Anlin</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>1413</th>
      <td>Aivley</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>44826</th>
      <td>Neymar</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>13289</th>
      <td>Cristaly</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>13257</th>
      <td>Crimsyn</td>
      <td>2014</td>
    </tr>
  </tbody>
</table>
</div>




```python
national_names_male_df=pd.merge(national_names_male_df,first_occurence_male, on="Name", how="left")
national_names_male_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>Name</th>
      <th>Year</th>
      <th>Gender</th>
      <th>Count</th>
      <th>Rank</th>
      <th>First Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>943</td>
      <td>John</td>
      <td>1880</td>
      <td>M</td>
      <td>9655</td>
      <td>1</td>
      <td>1880</td>
    </tr>
    <tr>
      <th>1</th>
      <td>944</td>
      <td>William</td>
      <td>1880</td>
      <td>M</td>
      <td>9532</td>
      <td>2</td>
      <td>1880</td>
    </tr>
    <tr>
      <th>2</th>
      <td>945</td>
      <td>James</td>
      <td>1880</td>
      <td>M</td>
      <td>5927</td>
      <td>3</td>
      <td>1880</td>
    </tr>
    <tr>
      <th>3</th>
      <td>946</td>
      <td>Charles</td>
      <td>1880</td>
      <td>M</td>
      <td>5348</td>
      <td>4</td>
      <td>1880</td>
    </tr>
    <tr>
      <th>4</th>
      <td>947</td>
      <td>George</td>
      <td>1880</td>
      <td>M</td>
      <td>5126</td>
      <td>5</td>
      <td>1880</td>
    </tr>
  </tbody>
</table>
</div>




```python
national_names_female_df=pd.merge(national_names_female_df,first_occurence_female, on="Name", how="left")
national_names_female_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>Name</th>
      <th>Year</th>
      <th>Gender</th>
      <th>Count</th>
      <th>Rank</th>
      <th>First Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Mary</td>
      <td>1880</td>
      <td>F</td>
      <td>7065</td>
      <td>1</td>
      <td>1880</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Anna</td>
      <td>1880</td>
      <td>F</td>
      <td>2604</td>
      <td>2</td>
      <td>1880</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Emma</td>
      <td>1880</td>
      <td>F</td>
      <td>2003</td>
      <td>3</td>
      <td>1880</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Elizabeth</td>
      <td>1880</td>
      <td>F</td>
      <td>1939</td>
      <td>4</td>
      <td>1880</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Minnie</td>
      <td>1880</td>
      <td>F</td>
      <td>1746</td>
      <td>5</td>
      <td>1880</td>
    </tr>
  </tbody>
</table>
</div>



##Determine the sum of all occurrences of each name and add to the master dataframe (Male & Female)


```python
total_occurence_male=national_names_male_df.groupby("Name").sum()
```


```python
total_occurence_male.reset_index(inplace=True)
total_occurence_male.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Id</th>
      <th>Year</th>
      <th>Count</th>
      <th>Rank</th>
      <th>First Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aaban</td>
      <td>11996737</td>
      <td>14076</td>
      <td>72</td>
      <td>56816</td>
      <td>14049</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aabid</td>
      <td>1452434</td>
      <td>2003</td>
      <td>5</td>
      <td>10889</td>
      <td>2003</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aadam</td>
      <td>33176772</td>
      <td>46051</td>
      <td>196</td>
      <td>179465</td>
      <td>45701</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aadan</td>
      <td>15054268</td>
      <td>18087</td>
      <td>112</td>
      <td>64495</td>
      <td>18027</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aadarsh</td>
      <td>22068238</td>
      <td>28095</td>
      <td>158</td>
      <td>97236</td>
      <td>28000</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_occurence_male.drop(['Id','Year','Rank','First Year'], axis=1, inplace=True)
total_occurence_male.columns = ['Name', 'Total Count']
total_occurence_male.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aaban</td>
      <td>72</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aabid</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aadam</td>
      <td>196</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aadan</td>
      <td>112</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aadarsh</td>
      <td>158</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_occurence_female=national_names_female_df.groupby("Name").sum()
```


```python
total_occurence_female.reset_index(inplace=True)
total_occurence_female.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Id</th>
      <th>Year</th>
      <th>Count</th>
      <th>Rank</th>
      <th>First Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aabha</td>
      <td>5250498</td>
      <td>6037</td>
      <td>21</td>
      <td>40974</td>
      <td>6033</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aabriella</td>
      <td>3414118</td>
      <td>4022</td>
      <td>10</td>
      <td>33866</td>
      <td>4016</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aaden</td>
      <td>1640162</td>
      <td>2009</td>
      <td>5</td>
      <td>17254</td>
      <td>2009</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aadhira</td>
      <td>5310611</td>
      <td>6039</td>
      <td>29</td>
      <td>33534</td>
      <td>6036</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aadhya</td>
      <td>13433441</td>
      <td>16084</td>
      <td>639</td>
      <td>43436</td>
      <td>16056</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_occurence_female.drop(['Id','Year','Rank','First Year'], axis=1, inplace=True)
total_occurence_female.columns = ['Name', 'Total Count']
total_occurence_female.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aabha</td>
      <td>21</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Aabriella</td>
      <td>10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Aaden</td>
      <td>5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Aadhira</td>
      <td>29</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aadhya</td>
      <td>639</td>
    </tr>
  </tbody>
</table>
</div>




```python
national_names_male_df=pd.merge(national_names_male_df,total_occurence_male, on="Name", how="left")
national_names_male_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>Name</th>
      <th>Year</th>
      <th>Gender</th>
      <th>Count</th>
      <th>Rank</th>
      <th>First Year</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>943</td>
      <td>John</td>
      <td>1880</td>
      <td>M</td>
      <td>9655</td>
      <td>1</td>
      <td>1880</td>
      <td>5084943</td>
    </tr>
    <tr>
      <th>1</th>
      <td>944</td>
      <td>William</td>
      <td>1880</td>
      <td>M</td>
      <td>9532</td>
      <td>2</td>
      <td>1880</td>
      <td>4055473</td>
    </tr>
    <tr>
      <th>2</th>
      <td>945</td>
      <td>James</td>
      <td>1880</td>
      <td>M</td>
      <td>5927</td>
      <td>3</td>
      <td>1880</td>
      <td>5105919</td>
    </tr>
    <tr>
      <th>3</th>
      <td>946</td>
      <td>Charles</td>
      <td>1880</td>
      <td>M</td>
      <td>5348</td>
      <td>4</td>
      <td>1880</td>
      <td>2364332</td>
    </tr>
    <tr>
      <th>4</th>
      <td>947</td>
      <td>George</td>
      <td>1880</td>
      <td>M</td>
      <td>5126</td>
      <td>5</td>
      <td>1880</td>
      <td>1454503</td>
    </tr>
  </tbody>
</table>
</div>




```python
national_names_female_df=pd.merge(national_names_female_df,total_occurence_female, on="Name", how="left")
national_names_female_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>Name</th>
      <th>Year</th>
      <th>Gender</th>
      <th>Count</th>
      <th>Rank</th>
      <th>First Year</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Mary</td>
      <td>1880</td>
      <td>F</td>
      <td>7065</td>
      <td>1</td>
      <td>1880</td>
      <td>4115282</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Anna</td>
      <td>1880</td>
      <td>F</td>
      <td>2604</td>
      <td>2</td>
      <td>1880</td>
      <td>873767</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Emma</td>
      <td>1880</td>
      <td>F</td>
      <td>2003</td>
      <td>3</td>
      <td>1880</td>
      <td>593970</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Elizabeth</td>
      <td>1880</td>
      <td>F</td>
      <td>1939</td>
      <td>4</td>
      <td>1880</td>
      <td>1601128</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Minnie</td>
      <td>1880</td>
      <td>F</td>
      <td>1746</td>
      <td>5</td>
      <td>1880</td>
      <td>158565</td>
    </tr>
  </tbody>
</table>
</div>



##Determine unique names (Male and Female) -- i.e., a list of all names that occur in the data set


```python
name_list_male = national_names_male_df["Name"].unique()
```


```python
name_list_male_df = pd.DataFrame(name_list_male)
```


```python
name_list_male_df.columns=["Name"]
name_list_male_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>John</td>
    </tr>
    <tr>
      <th>1</th>
      <td>William</td>
    </tr>
    <tr>
      <th>2</th>
      <td>James</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Charles</td>
    </tr>
    <tr>
      <th>4</th>
      <td>George</td>
    </tr>
  </tbody>
</table>
</div>




```python
name_list_female = national_names_female_df["Name"].unique()
```


```python
name_list_female_df = pd.DataFrame(name_list_female)
```


```python
name_list_female_df.columns=["Name"]
name_list_female_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Mary</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Anna</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Emma</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Elizabeth</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Minnie</td>
    </tr>
  </tbody>
</table>
</div>



##Save to new .csv files


```python
national_names_male_df.to_csv("Revised National Names Male.csv")
national_names_female_df.to_csv("Revised National Names Female.csv")
state_names_male_df.to_csv("Revised State Names Male.csv")
state_names_female_df.to_csv("Revised State Names Female.csv")
name_list_male_df.to_csv("All Male Names.csv")
name_list_female_df.to_csv("All Female Names.csv")
```
