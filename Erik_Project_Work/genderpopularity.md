
Observations:

Celebrities have a strong influence on names immediately when they become famous. They can have an effect on both males and females with that name.

In general, when a male version of a name increases, the female version will decrease. This is true for the opposite case as well.

Popular female names are more susceptible to sharper increases and declines than male names. The number of unique top male names has not changed nearly as much as the number of unique top female names due to there more gradual increases and decreases.


```python
#Dependencies 
import pandas as pd
import os
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns
```


```python
#Import Clean Data
data_file = os.path.join("Revised National Names Male.csv")
national_names_male_df = pd.read_csv(data_file)
data_file = os.path.join("Revised National Names Female.csv")
national_names_female_df = pd.read_csv(data_file)
national_names_male_df.head()
data_file = os.path.join("StateNames.csv")
state_names_df = pd.read_csv(data_file)
```


```python
#Drop id column from states
state_names_df.drop('Id', axis=1, inplace=True)
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
      <td>Mary</td>
      <td>1910</td>
      <td>F</td>
      <td>AK</td>
      <td>14</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Annie</td>
      <td>1910</td>
      <td>F</td>
      <td>AK</td>
      <td>12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anna</td>
      <td>1910</td>
      <td>F</td>
      <td>AK</td>
      <td>10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Margaret</td>
      <td>1910</td>
      <td>F</td>
      <td>AK</td>
      <td>8</td>
    </tr>
    <tr>
      <th>4</th>
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
#Drop unneeded column from national dataframes
national_names_male_df.drop('Unnamed: 0', axis=1, inplace=True)
national_names_female_df.drop('Unnamed: 0', axis=1, inplace=True)
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
#Merge Dataframes
df_merge = pd.merge(national_names_female_df, national_names_male_df, how='outer', left_on=['Name','Year'], right_on=['Name','Year'])
df_merge_needed = df_merge[['Name','Year', 'Count_x', 'Count_y']]
df_merge_needed.columns = ['Name','Year', 'Female Count', 'Male Count']
df_merge_needed.sort_values('Male Count', ascending = False).head()
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
      <th>Year</th>
      <th>Female Count</th>
      <th>Male Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>239187</th>
      <td>James</td>
      <td>1947</td>
      <td>257.0</td>
      <td>94755.0</td>
    </tr>
    <tr>
      <th>302925</th>
      <td>Michael</td>
      <td>1957</td>
      <td>254.0</td>
      <td>92709.0</td>
    </tr>
    <tr>
      <th>239225</th>
      <td>Robert</td>
      <td>1947</td>
      <td>236.0</td>
      <td>91642.0</td>
    </tr>
    <tr>
      <th>296031</th>
      <td>Michael</td>
      <td>1956</td>
      <td>244.0</td>
      <td>90633.0</td>
    </tr>
    <tr>
      <th>309894</th>
      <td>Michael</td>
      <td>1958</td>
      <td>295.0</td>
      <td>90519.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Find Names that are gender neutral 
total_names = df_merge_needed.groupby("Name").sum().sort_values('Female Count', ascending=False)
total_names['Total Counts']= total_names['Female Count']+total_names['Male Count']
total_names['Percentage Male']= total_names['Male Count']/total_names['Total Counts']*100
total_names = total_names.sort_values('Percentage Male', ascending=False)
total_names.head()
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
      <th>Year</th>
      <th>Female Count</th>
      <th>Male Count</th>
      <th>Total Counts</th>
      <th>Percentage Male</th>
    </tr>
    <tr>
      <th>Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Rocco</th>
      <td>242110</td>
      <td>5.0</td>
      <td>24812.0</td>
      <td>24817.0</td>
      <td>99.979853</td>
    </tr>
    <tr>
      <th>Matt</th>
      <td>262845</td>
      <td>5.0</td>
      <td>23399.0</td>
      <td>23404.0</td>
      <td>99.978636</td>
    </tr>
    <tr>
      <th>Doug</th>
      <td>170962</td>
      <td>5.0</td>
      <td>22454.0</td>
      <td>22459.0</td>
      <td>99.977737</td>
    </tr>
    <tr>
      <th>Ezekiel</th>
      <td>262845</td>
      <td>7.0</td>
      <td>30068.0</td>
      <td>30075.0</td>
      <td>99.976725</td>
    </tr>
    <tr>
      <th>Rodrigo</th>
      <td>188783</td>
      <td>5.0</td>
      <td>21385.0</td>
      <td>21390.0</td>
      <td>99.976625</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Only show top ten (by total count) names that are most gender neutral (40%-60%)
middle = total_names[(total_names['Percentage Male']<=60) & (total_names['Percentage Male']>=40)]
middle.sort_values('Total Counts', ascending = False).head(10)
middle.drop(['Year'], axis=1, inplace=True)
middle = middle.reset_index()
middle.sort_values('Total Counts', ascending = False).head(10)
```

    /anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:4: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
      after removing the cwd from sys.path.





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
      <th>Female Count</th>
      <th>Male Count</th>
      <th>Total Counts</th>
      <th>Percentage Male</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>47</th>
      <td>Casey</td>
      <td>75060.0</td>
      <td>108595.0</td>
      <td>183655.0</td>
      <td>59.129890</td>
    </tr>
    <tr>
      <th>412</th>
      <td>Riley</td>
      <td>81605.0</td>
      <td>87494.0</td>
      <td>169099.0</td>
      <td>51.741288</td>
    </tr>
    <tr>
      <th>711</th>
      <td>Jackie</td>
      <td>90337.0</td>
      <td>78148.0</td>
      <td>168485.0</td>
      <td>46.382764</td>
    </tr>
    <tr>
      <th>153</th>
      <td>Jaime</td>
      <td>49480.0</td>
      <td>65697.0</td>
      <td>115177.0</td>
      <td>57.040034</td>
    </tr>
    <tr>
      <th>871</th>
      <td>Peyton</td>
      <td>58567.0</td>
      <td>44037.0</td>
      <td>102604.0</td>
      <td>42.919379</td>
    </tr>
    <tr>
      <th>460</th>
      <td>Kerry</td>
      <td>48452.0</td>
      <td>49417.0</td>
      <td>97869.0</td>
      <td>50.493006</td>
    </tr>
    <tr>
      <th>238</th>
      <td>Frankie</td>
      <td>32355.0</td>
      <td>39894.0</td>
      <td>72249.0</td>
      <td>55.217373</td>
    </tr>
    <tr>
      <th>642</th>
      <td>Robbie</td>
      <td>22215.0</td>
      <td>20676.0</td>
      <td>42891.0</td>
      <td>48.205917</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Emerson</td>
      <td>13225.0</td>
      <td>19477.0</td>
      <td>32702.0</td>
      <td>59.559048</td>
    </tr>
    <tr>
      <th>158</th>
      <td>Carey</td>
      <td>12669.0</td>
      <td>16693.0</td>
      <td>29362.0</td>
      <td>56.852394</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Find largest change between years in male and female names
sorted_male_df = national_names_male_df.sort_values(['Name','Year'])
sorted_male_df['Change'] = abs(sorted_male_df.groupby('Name')['Count'].diff(1))
sorted_female_df = national_names_female_df.sort_values(['Name','Year'])
sorted_female_df['Change'] = abs(sorted_female_df.groupby('Name')['Count'].diff(1))
sorted_male_df.sort_values('Change', ascending = False).head(10)
sorted_male_df.drop(['Id'], axis=1, inplace=True)
sorted_female_df.drop(['Id'], axis=1, inplace=True)
```


```python
#Show top ten female names by size of change between years
top_changes_female = sorted_female_df.sort_values('Change', ascending = False).head(10)
top_changes_female
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
      <th>Year</th>
      <th>Gender</th>
      <th>Count</th>
      <th>Rank</th>
      <th>First Year</th>
      <th>Total Count</th>
      <th>Change</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>238672</th>
      <td>Linda</td>
      <td>1947</td>
      <td>F</td>
      <td>99680</td>
      <td>1</td>
      <td>1880</td>
      <td>1450843</td>
      <td>46972.0</td>
    </tr>
    <tr>
      <th>177025</th>
      <td>Shirley</td>
      <td>1935</td>
      <td>F</td>
      <td>42357</td>
      <td>2</td>
      <td>1880</td>
      <td>684656</td>
      <td>19521.0</td>
    </tr>
    <tr>
      <th>542928</th>
      <td>Ashley</td>
      <td>1983</td>
      <td>F</td>
      <td>33292</td>
      <td>4</td>
      <td>1917</td>
      <td>834720</td>
      <td>18444.0</td>
    </tr>
    <tr>
      <th>262992</th>
      <td>Deborah</td>
      <td>1951</td>
      <td>F</td>
      <td>42043</td>
      <td>4</td>
      <td>1880</td>
      <td>739273</td>
      <td>12972.0</td>
    </tr>
    <tr>
      <th>68512</th>
      <td>Mary</td>
      <td>1915</td>
      <td>F</td>
      <td>58187</td>
      <td>1</td>
      <td>1880</td>
      <td>4115282</td>
      <td>12843.0</td>
    </tr>
    <tr>
      <th>401339</th>
      <td>Jennifer</td>
      <td>1970</td>
      <td>F</td>
      <td>46160</td>
      <td>1</td>
      <td>1916</td>
      <td>1462742</td>
      <td>12455.0</td>
    </tr>
    <tr>
      <th>494304</th>
      <td>Amanda</td>
      <td>1979</td>
      <td>F</td>
      <td>31926</td>
      <td>3</td>
      <td>1880</td>
      <td>781807</td>
      <td>11406.0</td>
    </tr>
    <tr>
      <th>232986</th>
      <td>Linda</td>
      <td>1946</td>
      <td>F</td>
      <td>52708</td>
      <td>2</td>
      <td>1880</td>
      <td>1450843</td>
      <td>11243.0</td>
    </tr>
    <tr>
      <th>619594</th>
      <td>Brittany</td>
      <td>1989</td>
      <td>F</td>
      <td>37786</td>
      <td>3</td>
      <td>1963</td>
      <td>356473</td>
      <td>10971.0</td>
    </tr>
    <tr>
      <th>368980</th>
      <td>Michelle</td>
      <td>1966</td>
      <td>F</td>
      <td>27152</td>
      <td>4</td>
      <td>1915</td>
      <td>804495</td>
      <td>10937.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Show top ten male names by size of change between years
top_changes_male = sorted_male_df.sort_values('Change', ascending = False).head(10)
top_changes_male
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
      <th>Year</th>
      <th>Gender</th>
      <th>Count</th>
      <th>Rank</th>
      <th>First Year</th>
      <th>Total Count</th>
      <th>Change</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>188365</th>
      <td>Robert</td>
      <td>1946</td>
      <td>M</td>
      <td>84130</td>
      <td>2</td>
      <td>1880</td>
      <td>4796695</td>
      <td>14204.0</td>
    </tr>
    <tr>
      <th>188366</th>
      <td>John</td>
      <td>1946</td>
      <td>M</td>
      <td>79248</td>
      <td>3</td>
      <td>1880</td>
      <td>5084943</td>
      <td>13125.0</td>
    </tr>
    <tr>
      <th>188364</th>
      <td>James</td>
      <td>1946</td>
      <td>M</td>
      <td>87425</td>
      <td>1</td>
      <td>1880</td>
      <td>5105919</td>
      <td>12975.0</td>
    </tr>
    <tr>
      <th>188368</th>
      <td>Richard</td>
      <td>1946</td>
      <td>M</td>
      <td>58859</td>
      <td>5</td>
      <td>1880</td>
      <td>2555330</td>
      <td>12814.0</td>
    </tr>
    <tr>
      <th>192385</th>
      <td>David</td>
      <td>1947</td>
      <td>M</td>
      <td>57797</td>
      <td>6</td>
      <td>1880</td>
      <td>3577704</td>
      <td>11362.0</td>
    </tr>
    <tr>
      <th>188370</th>
      <td>Michael</td>
      <td>1946</td>
      <td>M</td>
      <td>41178</td>
      <td>7</td>
      <td>1880</td>
      <td>4309198</td>
      <td>11266.0</td>
    </tr>
    <tr>
      <th>41283</th>
      <td>John</td>
      <td>1912</td>
      <td>M</td>
      <td>24587</td>
      <td>1</td>
      <td>1880</td>
      <td>5084943</td>
      <td>11142.0</td>
    </tr>
    <tr>
      <th>271977</th>
      <td>John</td>
      <td>1965</td>
      <td>M</td>
      <td>71563</td>
      <td>2</td>
      <td>1880</td>
      <td>5084943</td>
      <td>10973.0</td>
    </tr>
    <tr>
      <th>295268</th>
      <td>Jason</td>
      <td>1970</td>
      <td>M</td>
      <td>27296</td>
      <td>13</td>
      <td>1880</td>
      <td>1014584</td>
      <td>10792.0</td>
    </tr>
    <tr>
      <th>172587</th>
      <td>James</td>
      <td>1942</td>
      <td>M</td>
      <td>77173</td>
      <td>1</td>
      <td>1880</td>
      <td>5105919</td>
      <td>10454.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Print out top ten tables
import six
def render_mpl_table(data, col_width=20.0, row_height=0.625, font_size=14,
                     header_color='#40466e', row_colors=['#f1f1f2', 'w'], edge_color='w',
                     bbox=[0, 0, 1, 1], header_columns=0,
                     ax=None, **kwargs):
    if ax is None:
        size = (np.array(data.shape[::-1]) + np.array([0, 1])) * np.array([col_width, row_height])
        fig, ax = plt.subplots(figsize=size)
        ax.axis('off')

    mpl_table = ax.table(cellText=data.values, bbox=bbox, colLabels=data.columns, **kwargs)

    mpl_table.auto_set_font_size(False)
    mpl_table.set_fontsize(font_size)

    for k, cell in six.iteritems(mpl_table._cells):
        cell.set_edgecolor(edge_color)
        if k[0] == 0 or k[1] < header_columns:
            cell.set_text_props(weight='bold', color='w')
            cell.set_facecolor(header_color)
        else:
            cell.set_facecolor(row_colors[k[0]%len(row_colors) ])
    return ax
fig = render_mpl_table(middle, header_columns=0, col_width=2.0)
plt.savefig('mostgenderneutral' +'.png')
```

    /anaconda3/lib/python3.6/site-packages/matplotlib/pyplot.py:523: RuntimeWarning: More than 20 figures have been opened. Figures created through the pyplot interface (`matplotlib.pyplot.figure`) are retained until explicitly closed and may consume too much memory. (To control this warning, see the rcParam `figure.max_open_warning`).
      max_open_warning, RuntimeWarning)



```python
fig = render_mpl_table(top_changes_female.head(10), header_columns=0, col_width=2.0)
plt.savefig('steepestfemaleincrease' +'.png')
```


```python
fig = render_mpl_table(top_changes_male.head(10), header_columns=0, col_width=2.0)
plt.savefig('steepestmaleincrease' +'.png')
```


```python
#Plot number of Jalens over time nationally

jalen_male = national_names_male_df[national_names_male_df['Name']=='Jalen'].sort_values('Year')
jalen_female = national_names_female_df[national_names_female_df['Name']=='Jalen'].sort_values('Year')

plt.figure(figsize=(20,8))
plt.rcParams.update({'font.size': 22})

with plt.style.context('seaborn-whitegrid'):
    male = plt.plot(jalen_male["Year"], jalen_male["Count"], marker = 'o', color = 'b')
    female = plt.plot(jalen_female["Year"], jalen_female["Count"], marker = 'o', color = 'pink')
    plt.xlabel("Year")
    plt.ylabel("Number of Names")
    plt.legend(["Males", "Females"])
    plt.title('Jalen')
    plt.savefig ('Jalen' +'.png')
    plt.show()

```


![png](output_14_0.png)



```python
#Plot number of Jalens over time in the state of Michigan

michigan_df = state_names_df[state_names_df['State']=='MI']
michigan_male_df = michigan_df[michigan_df['Gender']=='M']
michigan_female_df = michigan_df[michigan_df['Gender']=='F']
jalen_male = michigan_male_df[michigan_male_df['Name']=='Jalen'].sort_values('Year')
jalen_female = michigan_female_df[michigan_female_df['Name']=='Jalen'].sort_values('Year')

plt.figure(figsize=(20,8))
plt.rcParams.update({'font.size': 22})

with plt.style.context('seaborn-whitegrid'):
    male = plt.plot(jalen_male["Year"], jalen_male["Count"], marker = 'o', color = 'b')
    female = plt.plot(jalen_female["Year"], jalen_female["Count"], marker = 'o', color = 'pink')
    plt.xlabel("Year")
    plt.ylabel("Number of Names")
    plt.legend(["Males", "Females"])
    plt.title('Jalen')
    plt.xlim(1975, 2015)
    plt.savefig ('JalenMI' +'.png')
    plt.show()

```


![png](output_15_0.png)



```python
#Plot number of Jasons over time nationally

jason_male = national_names_male_df[national_names_male_df['Name']=='Jason'].sort_values('Year')
jason_female = national_names_female_df[national_names_female_df['Name']=='Jason'].sort_values('Year')

plt.figure(figsize=(20,8))
plt.rcParams.update({'font.size': 22})

with plt.style.context('seaborn-whitegrid'):
    male = plt.plot(jason_male["Year"], jason_male["Count"], marker = 'o', color = 'b')
    female = plt.plot(jason_female["Year"], jason_female["Count"], marker = 'o', color = 'pink')
    plt.xlabel("Year")
    plt.ylabel("Number of Names")
    plt.legend(["Males", "Females"])
    plt.title('Jason')
    plt.savefig ('Jason' +'.png')
    plt.show()

```


![png](output_16_0.png)



```python
#Plot number of Shirleys over time nationally

shirley_male = national_names_male_df[national_names_male_df['Name']=='Shirley'].sort_values('Year')
shirley_female = national_names_female_df[national_names_female_df['Name']=='Shirley'].sort_values('Year')

plt.figure(figsize=(20,8))
plt.rcParams.update({'font.size': 22})

with plt.style.context('seaborn-whitegrid'):
    male = plt.plot(shirley_male["Year"], shirley_male["Count"], marker = 'o', color = 'b')
    female = plt.plot(shirley_female["Year"], shirley_female["Count"], marker = 'o', color = 'pink')
    plt.xlabel("Year")
    plt.ylabel("Number of Names")
    plt.legend(["Males", "Females"])
    plt.title('Shirley')
    plt.savefig ('Shirley' +'.png')
    plt.show()
```


![png](output_17_0.png)



```python
#Plot number of Rileys over time nationally

riley_male = national_names_male_df[national_names_male_df['Name']=='Riley'].sort_values('Year')
riley_female = national_names_female_df[national_names_female_df['Name']=='Riley'].sort_values('Year')

plt.figure(figsize=(20,8))
plt.rcParams.update({'font.size': 22})

with plt.style.context('seaborn-whitegrid'):
    male = plt.plot(riley_male["Year"], riley_male["Count"], marker = 'o', color = 'b')
    female = plt.plot(riley_female["Year"], riley_female["Count"], marker = 'o', color = 'pink')
    plt.xlabel("Year")
    plt.ylabel("Number of Names")
    plt.legend(["Males", "Females"])
    plt.title('Riley')
    plt.savefig ('Riley' +'.png')
    plt.show()

```


![png](output_18_0.png)



```python
#Plot number of Kerrys over time nationally

kerry_male = national_names_male_df[national_names_male_df['Name']=='Kerry'].sort_values('Year')
kerry_female = national_names_female_df[national_names_female_df['Name']=='Kerry'].sort_values('Year')

plt.figure(figsize=(20,8))
plt.rcParams.update({'font.size': 22})

with plt.style.context('seaborn-whitegrid'):
    male = plt.plot(kerry_male["Year"], kerry_male["Count"], marker = 'o', color = 'b')
    female = plt.plot(kerry_female["Year"], kerry_female["Count"], marker = 'o', color = 'pink')
    plt.xlabel("Year")
    plt.ylabel("Number of Names")
    plt.legend(["Males", "Females"])
    plt.title('Kerry')
    plt.xlim(1910, 2020)
    plt.savefig ('Kerry' +'.png')
    plt.show()

```


![png](output_19_0.png)



```python
#Plot number of Frankies over time nationally  (include famous Frankies)

frankie_male = national_names_male_df[national_names_male_df['Name']=='Frankie'].sort_values('Year')
frankie_female = national_names_female_df[national_names_female_df['Name']=='Frankie'].sort_values('Year')

plt.figure(figsize=(20,8))
plt.rcParams.update({'font.size': 22})

with plt.style.context('seaborn-whitegrid'):
    male = plt.plot(frankie_male["Year"], frankie_male["Count"], marker = 'o', color = 'b')
    female = plt.plot(frankie_female["Year"], frankie_female["Count"], marker = 'o', color = 'pink')
    plt.xlabel("Year")
    plt.ylabel("Number of Names")
    plt.legend(["Males", "Females"])
    plt.title('Frankie')    
    plt.axvline(1960)
    plt.text(1961.5, 810,'Frankie Valli\nFrankie Avalon')
    plt.savefig ('Frankie' +'.png')
    plt.show()
```


![png](output_20_0.png)



```python
#Plot number of Jackies over time nationally (include famous Jackies)

jackie_male = national_names_male_df[national_names_male_df['Name']=='Jackie'].sort_values('Year')
jackie_female = national_names_female_df[national_names_female_df['Name']=='Jackie'].sort_values('Year')

plt.figure(figsize=(20,8))
plt.rcParams.update({'font.size': 22})

with plt.style.context('seaborn-whitegrid'):
    male = plt.plot(jackie_male["Year"], jackie_male["Count"], marker = 'o', color = 'b')
    female = plt.plot(jackie_female["Year"], jackie_female["Count"], marker = 'o', color = 'pink')
    plt.xlabel("Year")
    plt.ylabel("Number of Names")
    plt.legend(["Males", "Females"])
    plt.title('Jackie')
    plt.axvline(1947)
    plt.axvline(1931)
    plt.axvline(1960)
    plt.text(1928.5, 2800,'Jackie Robinson' + '\n' + '         MLB debut')
    plt.text(1915, 1800,'Jackie Cooper' + '\n' + '     nominated' + '\n' + '        for Oscar')
    plt.text(1942, 3800,'Jackie Kennedy' + '\n' + '           becomes' + '\n' + '            first lady')
    plt.savefig ('Jackie' +'.png')

    plt.show()
```


![png](output_21_0.png)



```python
#Plot number of Jesses over time nationally (include alternate spellings)

jesse_male = national_names_male_df[national_names_male_df['Name']=='Jesse'].sort_values('Year')
jesse_female = national_names_female_df[national_names_female_df['Name']=='Jesse'].sort_values('Year')
jessie_male = national_names_male_df[national_names_male_df['Name']=='Jessie'].sort_values('Year')
jessie_female = national_names_female_df[national_names_female_df['Name']=='Jessie'].sort_values('Year')

plt.figure(figsize=(20,8))
plt.rcParams.update({'font.size': 22})

with plt.style.context('seaborn-whitegrid'):
    male = plt.plot(jessie_male["Year"], jessie_male["Count"], marker = 'o', color = 'b')
    female = plt.plot(jessie_female["Year"], jessie_female["Count"], marker = 'o', color = 'pink')  
    alt_male = plt.plot(jesse_male["Year"], jesse_male["Count"], marker = 'o', color = 'green')
    alt_female = plt.plot(jesse_female["Year"], jesse_female["Count"], marker = 'o', color = 'purple')
    plt.xlabel("Year")
    plt.ylabel("Number of Names")
    plt.legend(["Jessie (M)", "Jessie (F)", "Jesse (M)", "Jesse (F)"])
    plt.savefig ('Jessie' +'.png')
    plt.show()
```


![png](output_22_0.png)



```python
#Plot number of Jamies over time nationally

jaime_male = national_names_male_df[national_names_male_df['Name']=='Jaime'].sort_values('Year')
jaime_female = national_names_female_df[national_names_female_df['Name']=='Jaime'].sort_values('Year')

plt.figure(figsize=(20,8))
plt.rcParams.update({'font.size': 22})

with plt.style.context('seaborn-whitegrid'):
    male = plt.plot(jaime_male["Year"], jaime_male["Count"], marker = 'o', color = 'b')
    female = plt.plot(jaime_female["Year"], jaime_female["Count"], marker = 'o', color = 'pink')
    plt.xlabel("Year")
    plt.ylabel("Number of Names")
    plt.legend(["Males", "Females"])
    plt.title('Jamie')    
    plt.savefig ('Jaime' +'.png')
    plt.show()

```


![png](output_23_0.png)



```python
#Plot number of Robbies over time nationally

robbie_male = national_names_male_df[national_names_male_df['Name']=='Robbie'].sort_values('Year')
robbie_female = national_names_female_df[national_names_female_df['Name']=='Robbie'].sort_values('Year')

plt.figure(figsize=(20,8))
plt.rcParams.update({'font.size': 22})

with plt.style.context('seaborn-whitegrid'):
    male = plt.plot(robbie_male["Year"], robbie_male["Count"], marker = 'o', color = 'b')
    female = plt.plot(robbie_female["Year"], robbie_female["Count"], marker = 'o', color = 'pink')
    plt.xlabel("Year")
    plt.ylabel("Number of Names")
    plt.legend(["Males", "Females"])
    plt.title('Robbie')
    plt.axvline(1975)
    plt.text(1958, 7800,'                Debut of' + '\n' + 'My Three Sons')
    plt.savefig ('Robbie' +'.png')
    plt.show()

```


![png](output_24_0.png)



```python
#Plot number of Sheas over time nationally (include alternate spellings)

shea_male = national_names_male_df[national_names_male_df['Name']=='Shea'].sort_values('Year')
shea_female = national_names_female_df[national_names_female_df['Name']=='Shea'].sort_values('Year')
shay_male = national_names_male_df[national_names_male_df['Name']=='Shay'].sort_values('Year')
shay_female = national_names_female_df[national_names_female_df['Name']=='Shay'].sort_values('Year')

plt.figure(figsize=(20,8))
plt.rcParams.update({'font.size': 22})

with plt.style.context('seaborn-whitegrid'):
    male = plt.plot(shay_male["Year"], shay_male["Count"], marker = 'o', color = 'b')
    female = plt.plot(shay_female["Year"], shay_female["Count"], marker = 'o', color = 'pink')  
    alt_male = plt.plot(shea_male["Year"], shea_male["Count"], marker = 'o', color = 'green')
    alt_female = plt.plot(shea_female["Year"], shea_female["Count"], marker = 'o', color = 'purple')

    plt.xlabel("Year")
    plt.ylabel("Number of Names")
    plt.legend(["Shay (M)", "Shay (F)", "Shea (M)", "Shea (F)"])
    plt.savefig ('Shay' +'.png')
    plt.xlim(1920, 2020)
    plt.show()

```


![png](output_25_0.png)



```python
#Plot number of Jesses over time nationally (include alternate spellings and famous Jaime)

jaime_male = national_names_male_df[national_names_male_df['Name']=='Jaime'].sort_values('Year')
jaime_female = national_names_female_df[national_names_female_df['Name']=='Jaime'].sort_values('Year')
jamie_male = national_names_male_df[national_names_male_df['Name']=='Jamie'].sort_values('Year')
jamie_female = national_names_female_df[national_names_female_df['Name']=='Jamie'].sort_values('Year')

plt.figure(figsize=(20,8))
plt.rcParams.update({'font.size': 22})

with plt.style.context('seaborn-whitegrid'):
    male = plt.plot(jamie_male["Year"], jamie_male["Count"], marker = 'o', color = 'b')
    female = plt.plot(jamie_female["Year"], jamie_female["Count"], marker = 'o', color = 'pink')  
    alt_male = plt.plot(jaime_male["Year"], jaime_male["Count"], marker = 'o', color = 'green')
    alt_female = plt.plot(jaime_female["Year"], jaime_female["Count"], marker = 'o', color = 'purple')
    plt.xlabel("Year")
    plt.ylabel("Number of Names")
    plt.legend(["Jamie (M)", "Jamie (F)", "Jaime (M)", "Jaime (F)"])
    plt.xlim(1920, 2020)
    plt.axvline(1975)
    plt.text(1958, 7800,'                Debut of' + '\n' + 'The Bionic Woman')
    plt.savefig ('Jamie' +'.png')
    plt.show()
```


![png](output_26_0.png)



```python
#Plot number of Jesses over time nationally (include alternate spellings and famous Robbie)

robby_male = national_names_male_df[national_names_male_df['Name']=='Robby'].sort_values('Year')
robby_female = national_names_female_df[national_names_female_df['Name']=='Robby'].sort_values('Year')
robbie_male = national_names_male_df[national_names_male_df['Name']=='Robbie'].sort_values('Year')
robbie_female = national_names_female_df[national_names_female_df['Name']=='Robbie'].sort_values('Year')

plt.figure(figsize=(20,8))
plt.rcParams.update({'font.size': 22})

with plt.style.context('seaborn-whitegrid'):
    male = plt.plot(robbie_male["Year"], robbie_male["Count"], marker = 'o', color = 'b')
    female = plt.plot(robbie_female["Year"], robbie_female["Count"], marker = 'o', color = 'pink')  
    alt_male = plt.plot(robby_male["Year"], robby_male["Count"], marker = 'o', color = 'green')
    alt_female = plt.plot(robby_female["Year"], robby_female["Count"], marker = 'o', color = 'purple')

    plt.xlabel("Year")
    plt.ylabel("Number of Names")
    plt.legend(["Robbie (M)", "Robbie (F)", "Robby (M)", "Robby (F)"])
    plt.axvline(1960)
    plt.text(1940, 760,'           Debut of' + '\n' + 'My Three Sons')
    plt.savefig ('Robbie' +'.png')
    plt.show()

```


![png](output_27_0.png)



```python
#Plot number of alternates to Robbie over time nationally (include alternate spellings)

robert_male = national_names_male_df[national_names_male_df['Name']=='Robert'].sort_values('Year')
robert_female = national_names_female_df[national_names_female_df['Name']=='Robert'].sort_values('Year')
rob_male = national_names_male_df[national_names_male_df['Name']=='Rob'].sort_values('Year')
rob_female = national_names_female_df[national_names_female_df['Name']=='Rob'].sort_values('Year')

plt.figure(figsize=(20,8))
plt.rcParams.update({'font.size': 22})

with plt.style.context('seaborn-whitegrid'):
    male = plt.plot(rob_male["Year"], rob_male["Count"], marker = 'o', color = 'b')
    female = plt.plot(rob_female["Year"], rob_female["Count"], marker = 'o', color = 'pink')  
    alt_male = plt.plot(robert_male["Year"], robert_male["Count"], marker = 'o', color = 'green')
    alt_female = plt.plot(robert_female["Year"], robert_female["Count"], marker = 'o', color = 'purple')

    plt.xlabel("Year")
    plt.ylabel("Number of Names")
    plt.legend(["Rob (M)", "Rob (F)", "Robert (M)", "Robert (F)"])
    plt.savefig ('Rob' +'.png')
    plt.xlim(1920, 2020)
    plt.show()

```


![png](output_28_0.png)

