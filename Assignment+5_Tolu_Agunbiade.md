

```python
#import modules
import pandas as pd
import numpy as np
import sqlite3 as sql
import json
```


```python
#Read the csv file into pandas dataframe
file = pd.read_csv("C:\Users\Tolu\Downloads\HateCrimes_csv.csv")
file.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>State</th>
      <th>Agency_type</th>
      <th>Agency_name</th>
      <th>Ethnicity</th>
      <th>Disability</th>
      <th>Gender</th>
      <th>Gender_Identity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alabama</td>
      <td>Cities</td>
      <td>Florence</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alabama</td>
      <td>Cities</td>
      <td>Hoover</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alabama</td>
      <td>Cities</td>
      <td>Prattville</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alabama</td>
      <td>Cities</td>
      <td>Tuscaloosa</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alaska</td>
      <td>Cities</td>
      <td>Anchorage</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Confirm number of columns and rows for the csv file
file.shape
```




    (1826, 7)




```python
#Read the json file into pandas dataframe
file_json = pd.read_json("C:\Users\Tolu\Downloads\HateCrimes_json.json")
file_json
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Agency_name</th>
      <th>Agency_type</th>
      <th>Population</th>
      <th>State</th>
      <th>quarter_1</th>
      <th>quarter_2</th>
      <th>quarter_3</th>
      <th>quarter_4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Florence</td>
      <td>Cities</td>
      <td>39481</td>
      <td>Alabama</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Hoover</td>
      <td>Cities</td>
      <td>84139</td>
      <td>Alabama</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Prattville</td>
      <td>Cities</td>
      <td>35154</td>
      <td>Alabama</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Tuscaloosa</td>
      <td>Cities</td>
      <td>94126</td>
      <td>Alabama</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Anchorage</td>
      <td>Cities</td>
      <td>299455</td>
      <td>Alaska</td>
      <td>2</td>
      <td>3</td>
      <td>3</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Apache Junction</td>
      <td>Cities</td>
      <td>36626</td>
      <td>Arizona</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Avondale</td>
      <td>Cities</td>
      <td>78905</td>
      <td>Arizona</td>
      <td>1</td>
      <td>1</td>
      <td>3</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Eagar</td>
      <td>Cities</td>
      <td>5034</td>
      <td>Arizona</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>El Mirage</td>
      <td>Cities</td>
      <td>32837</td>
      <td>Arizona</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Gilbert</td>
      <td>Cities</td>
      <td>225232</td>
      <td>Arizona</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Glendale</td>
      <td>Cities</td>
      <td>234006</td>
      <td>Arizona</td>
      <td>2</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Goodyear</td>
      <td>Cities</td>
      <td>71048</td>
      <td>Arizona</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Maricopa</td>
      <td>Cities</td>
      <td>44871</td>
      <td>Arizona</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Mesa</td>
      <td>Cities</td>
      <td>456155</td>
      <td>Arizona</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Phoenix</td>
      <td>Cities</td>
      <td>1502139</td>
      <td>Arizona</td>
      <td>25</td>
      <td>21</td>
      <td>35</td>
      <td>0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Prescott</td>
      <td>Cities</td>
      <td>40752</td>
      <td>Arizona</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Scottsdale</td>
      <td>Cities</td>
      <td>225523</td>
      <td>Arizona</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Tempe</td>
      <td>Cities</td>
      <td>168501</td>
      <td>Arizona</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Tucson</td>
      <td>Cities</td>
      <td>525486</td>
      <td>Arizona</td>
      <td>8</td>
      <td>8</td>
      <td>6</td>
      <td>4</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Yuma</td>
      <td>Cities</td>
      <td>96014</td>
      <td>Arizona</td>
      <td>3</td>
      <td>5</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Northern Arizona University</td>
      <td>Universities and Colleges</td>
      <td>25991</td>
      <td>Arizona</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>21</th>
      <td>University of Arizona</td>
      <td>Universities and Colleges</td>
      <td>40223</td>
      <td>Arizona</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Cochise</td>
      <td>Metropolitan Counties</td>
      <td>0</td>
      <td>Arizona</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Maricopa</td>
      <td>Metropolitan Counties</td>
      <td>0</td>
      <td>Arizona</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Pima</td>
      <td>Metropolitan Counties</td>
      <td>0</td>
      <td>Arizona</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Yuma</td>
      <td>Metropolitan Counties</td>
      <td>0</td>
      <td>Arizona</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Bentonville</td>
      <td>Cities</td>
      <td>39132</td>
      <td>Arkansas</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Berryville</td>
      <td>Cities</td>
      <td>5417</td>
      <td>Arkansas</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Cabot</td>
      <td>Cities</td>
      <td>24695</td>
      <td>Arkansas</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>England</td>
      <td>Cities</td>
      <td>2806</td>
      <td>Arkansas</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
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
    </tr>
    <tr>
      <th>1796</th>
      <td>Moundsville</td>
      <td>Cities</td>
      <td>9130</td>
      <td>West_Virginia</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1797</th>
      <td>Oak Hill</td>
      <td>Cities</td>
      <td>7709</td>
      <td>West_Virginia</td>
      <td>0</td>
      <td>6</td>
      <td>8</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1798</th>
      <td>Wellsburg</td>
      <td>Cities</td>
      <td>2760</td>
      <td>West_Virginia</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1799</th>
      <td>Brooke</td>
      <td>Metropolitan Counties</td>
      <td>0</td>
      <td>West_Virginia</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1800</th>
      <td>Fayette</td>
      <td>Metropolitan Counties</td>
      <td>0</td>
      <td>West_Virginia</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1801</th>
      <td>Hancock</td>
      <td>Metropolitan Counties</td>
      <td>0</td>
      <td>West_Virginia</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1802</th>
      <td>Harrison</td>
      <td>Nonmetropolitan Counties</td>
      <td>0</td>
      <td>West_Virginia</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1803</th>
      <td>McDowell</td>
      <td>Nonmetropolitan Counties</td>
      <td>0</td>
      <td>West_Virginia</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1804</th>
      <td>Algoma</td>
      <td>Cities</td>
      <td>3143</td>
      <td>Wisconsin</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1805</th>
      <td>Appleton</td>
      <td>Cities</td>
      <td>73141</td>
      <td>Wisconsin</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1806</th>
      <td>Burlington</td>
      <td>Cities</td>
      <td>10502</td>
      <td>Wisconsin</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1807</th>
      <td>Fond du Lac</td>
      <td>Cities</td>
      <td>43042</td>
      <td>Wisconsin</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1808</th>
      <td>Green Bay</td>
      <td>Cities</td>
      <td>105107</td>
      <td>Wisconsin</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1809</th>
      <td>Janesville</td>
      <td>Cities</td>
      <td>63603</td>
      <td>Wisconsin</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1810</th>
      <td>La Crosse</td>
      <td>Cities</td>
      <td>51741</td>
      <td>Wisconsin</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1811</th>
      <td>Madison</td>
      <td>Cities</td>
      <td>242523</td>
      <td>Wisconsin</td>
      <td>3</td>
      <td>5</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1812</th>
      <td>Merrill</td>
      <td>Cities</td>
      <td>9427</td>
      <td>Wisconsin</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1813</th>
      <td>Milwaukee</td>
      <td>Cities</td>
      <td>600805</td>
      <td>Wisconsin</td>
      <td>1</td>
      <td>3</td>
      <td>4</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1814</th>
      <td>Oak Creek</td>
      <td>Cities</td>
      <td>35046</td>
      <td>Wisconsin</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1815</th>
      <td>River Falls</td>
      <td>Cities</td>
      <td>15227</td>
      <td>Wisconsin</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1816</th>
      <td>Sparta</td>
      <td>Cities</td>
      <td>9623</td>
      <td>Wisconsin</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1817</th>
      <td>Wausau</td>
      <td>Cities</td>
      <td>39176</td>
      <td>Wisconsin</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1818</th>
      <td>"University of Wisconsin</td>
      <td>Universities and Colleges</td>
      <td>0</td>
      <td>Wisconsin</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1819</th>
      <td>Dane</td>
      <td>Metropolitan Counties</td>
      <td>0</td>
      <td>Wisconsin</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1820</th>
      <td>Burnett</td>
      <td>Nonmetropolitan Counties</td>
      <td>0</td>
      <td>Wisconsin</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1821</th>
      <td>Grant</td>
      <td>Nonmetropolitan Counties</td>
      <td>0</td>
      <td>Wisconsin</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1822</th>
      <td>Lincoln</td>
      <td>Nonmetropolitan Counties</td>
      <td>0</td>
      <td>Wisconsin</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1823</th>
      <td>Manitowoc</td>
      <td>Nonmetropolitan Counties</td>
      <td>0</td>
      <td>Wisconsin</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1824</th>
      <td>Oneida</td>
      <td>Nonmetropolitan Counties</td>
      <td>0</td>
      <td>Wisconsin</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1825</th>
      <td>Gillette</td>
      <td>Cities</td>
      <td>31884</td>
      <td>Wyoming</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>1826 rows × 8 columns</p>
</div>




```python
#Confirm number of columns and rows for the json file
file_json.shape
```




    (1826, 8)




```python
#Set a variable for the .db file
hate_sql = "C:/Users/Tolu/Downloads/hatecrimes.db"
```


```python
#Connecting the sql 
conn = sql.connect(hate_sql)
```


```python
#create a cursor function for the .db file
c = conn.cursor()
```


```python
# Executing sql query to select data from the crimes table in the .db file
data_1 = c.execute('SELECT * FROM crimes')
```


```python
# Getting the data into python
data_2 = data_1.fetchall()
```


```python
# Turning sql data frame into pandas and display data_3
data_3 = pd.DataFrame(data_2)
data_3
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alabama</td>
      <td>Cities</td>
      <td>Florence</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alabama</td>
      <td>Cities</td>
      <td>Hoover</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alabama</td>
      <td>Cities</td>
      <td>Prattville</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alabama</td>
      <td>Cities</td>
      <td>Tuscaloosa</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alaska</td>
      <td>Cities</td>
      <td>Anchorage</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Arizona</td>
      <td>Cities</td>
      <td>Apache Junction</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Arizona</td>
      <td>Cities</td>
      <td>Avondale</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Arizona</td>
      <td>Cities</td>
      <td>Eagar</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Arizona</td>
      <td>Cities</td>
      <td>El Mirage</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Arizona</td>
      <td>Cities</td>
      <td>Gilbert</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Arizona</td>
      <td>Cities</td>
      <td>Glendale</td>
      <td>2</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Arizona</td>
      <td>Cities</td>
      <td>Goodyear</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Arizona</td>
      <td>Cities</td>
      <td>Maricopa</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Arizona</td>
      <td>Cities</td>
      <td>Mesa</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Arizona</td>
      <td>Cities</td>
      <td>Phoenix</td>
      <td>40</td>
      <td>12</td>
      <td>14</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Arizona</td>
      <td>Cities</td>
      <td>Prescott</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Arizona</td>
      <td>Cities</td>
      <td>Scottsdale</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Arizona</td>
      <td>Cities</td>
      <td>Tempe</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Arizona</td>
      <td>Cities</td>
      <td>Tucson</td>
      <td>13</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Arizona</td>
      <td>Cities</td>
      <td>Yuma</td>
      <td>3</td>
      <td>4</td>
      <td>0</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Arizona</td>
      <td>Universities and Colleges</td>
      <td>Northern Arizona University</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Arizona</td>
      <td>Universities and Colleges</td>
      <td>University of Arizona</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Arizona</td>
      <td>Metropolitan Counties</td>
      <td>Cochise</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Arizona</td>
      <td>Metropolitan Counties</td>
      <td>Maricopa</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Arizona</td>
      <td>Metropolitan Counties</td>
      <td>Pima</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Arizona</td>
      <td>Metropolitan Counties</td>
      <td>Yuma</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Arkansas</td>
      <td>Cities</td>
      <td>Bentonville</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Arkansas</td>
      <td>Cities</td>
      <td>Berryville</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Arkansas</td>
      <td>Cities</td>
      <td>Cabot</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Arkansas</td>
      <td>Cities</td>
      <td>England</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1796</th>
      <td>West_Virginia</td>
      <td>Cities</td>
      <td>Moundsville</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1797</th>
      <td>West_Virginia</td>
      <td>Cities</td>
      <td>Oak Hill</td>
      <td>14</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1798</th>
      <td>West_Virginia</td>
      <td>Cities</td>
      <td>Wellsburg</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1799</th>
      <td>West_Virginia</td>
      <td>Metropolitan Counties</td>
      <td>Brooke</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1800</th>
      <td>West_Virginia</td>
      <td>Metropolitan Counties</td>
      <td>Fayette</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1801</th>
      <td>West_Virginia</td>
      <td>Metropolitan Counties</td>
      <td>Hancock</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1802</th>
      <td>West_Virginia</td>
      <td>Nonmetropolitan Counties</td>
      <td>Harrison</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1803</th>
      <td>West_Virginia</td>
      <td>Nonmetropolitan Counties</td>
      <td>McDowell</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1804</th>
      <td>Wisconsin</td>
      <td>Cities</td>
      <td>Algoma</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1805</th>
      <td>Wisconsin</td>
      <td>Cities</td>
      <td>Appleton</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1806</th>
      <td>Wisconsin</td>
      <td>Cities</td>
      <td>Burlington</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1807</th>
      <td>Wisconsin</td>
      <td>Cities</td>
      <td>Fond du Lac</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1808</th>
      <td>Wisconsin</td>
      <td>Cities</td>
      <td>Green Bay</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1809</th>
      <td>Wisconsin</td>
      <td>Cities</td>
      <td>Janesville</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1810</th>
      <td>Wisconsin</td>
      <td>Cities</td>
      <td>La Crosse</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1811</th>
      <td>Wisconsin</td>
      <td>Cities</td>
      <td>Madison</td>
      <td>3</td>
      <td>1</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1812</th>
      <td>Wisconsin</td>
      <td>Cities</td>
      <td>Merrill</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1813</th>
      <td>Wisconsin</td>
      <td>Cities</td>
      <td>Milwaukee</td>
      <td>5</td>
      <td>1</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1814</th>
      <td>Wisconsin</td>
      <td>Cities</td>
      <td>Oak Creek</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1815</th>
      <td>Wisconsin</td>
      <td>Cities</td>
      <td>River Falls</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1816</th>
      <td>Wisconsin</td>
      <td>Cities</td>
      <td>Sparta</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1817</th>
      <td>Wisconsin</td>
      <td>Cities</td>
      <td>Wausau</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1818</th>
      <td>Wisconsin</td>
      <td>Universities and Colleges</td>
      <td>University of Wisconsin, Platteville</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1819</th>
      <td>Wisconsin</td>
      <td>Metropolitan Counties</td>
      <td>Dane</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1820</th>
      <td>Wisconsin</td>
      <td>Nonmetropolitan Counties</td>
      <td>Burnett</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1821</th>
      <td>Wisconsin</td>
      <td>Nonmetropolitan Counties</td>
      <td>Grant</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1822</th>
      <td>Wisconsin</td>
      <td>Nonmetropolitan Counties</td>
      <td>Lincoln</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1823</th>
      <td>Wisconsin</td>
      <td>Nonmetropolitan Counties</td>
      <td>Manitowoc</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1824</th>
      <td>Wisconsin</td>
      <td>Nonmetropolitan Counties</td>
      <td>Oneida</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1825</th>
      <td>Wyoming</td>
      <td>Cities</td>
      <td>Gillette</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>1826 rows × 6 columns</p>
</div>




```python
#Confirm number of columns and rows for the crimes data
data_3.shape
```




    (1826, 6)




```python
#Change column headers of crimes data to match the header of the json and csv file
data_3.columns = ['State', 'Agency_type', 'Agency_name', 'Total_3', 'Total_4', 'Total_5']
```


```python
#Check header of crimes data
data_3.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>State</th>
      <th>Agency_type</th>
      <th>Agency_name</th>
      <th>Total_3</th>
      <th>Total_4</th>
      <th>Total_5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alabama</td>
      <td>Cities</td>
      <td>Florence</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alabama</td>
      <td>Cities</td>
      <td>Hoover</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Alabama</td>
      <td>Cities</td>
      <td>Prattville</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Alabama</td>
      <td>Cities</td>
      <td>Tuscaloosa</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Alaska</td>
      <td>Cities</td>
      <td>Anchorage</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Merge csv data with the json data 
new_data = pd.merge(dude, file,on=('Agency_name', 'Agency_type', 'State'), how='inner')
new_data.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Agency_name</th>
      <th>Agency_type</th>
      <th>Population</th>
      <th>State</th>
      <th>quarter_1</th>
      <th>quarter_2</th>
      <th>quarter_3</th>
      <th>quarter_4</th>
      <th>Ethnicity</th>
      <th>Disability</th>
      <th>Gender</th>
      <th>Gender_Identity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Florence</td>
      <td>Cities</td>
      <td>39481</td>
      <td>Alabama</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Hoover</td>
      <td>Cities</td>
      <td>84139</td>
      <td>Alabama</td>
      <td>0</td>
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
      <td>Prattville</td>
      <td>Cities</td>
      <td>35154</td>
      <td>Alabama</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Tuscaloosa</td>
      <td>Cities</td>
      <td>94126</td>
      <td>Alabama</td>
      <td>0</td>
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
      <td>Anchorage</td>
      <td>Cities</td>
      <td>299455</td>
      <td>Alaska</td>
      <td>2</td>
      <td>3</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#confirm number of rows and columns in the merged data
new_data.shape
```




    (1828, 12)




```python
#merge the crimes data with the original merged data
final_data = pd.merge(new_data, data_3 ,on=('Agency_name', 'Agency_type', 'State'), how='inner')
final_data.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Agency_name</th>
      <th>Agency_type</th>
      <th>Population</th>
      <th>State</th>
      <th>quarter_1</th>
      <th>quarter_2</th>
      <th>quarter_3</th>
      <th>quarter_4</th>
      <th>Ethnicity</th>
      <th>Disability</th>
      <th>Gender</th>
      <th>Gender_Identity</th>
      <th>Total_3</th>
      <th>Total_4</th>
      <th>Total_5</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Florence</td>
      <td>Cities</td>
      <td>39481</td>
      <td>Alabama</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Hoover</td>
      <td>Cities</td>
      <td>84139</td>
      <td>Alabama</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Prattville</td>
      <td>Cities</td>
      <td>35154</td>
      <td>Alabama</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Tuscaloosa</td>
      <td>Cities</td>
      <td>94126</td>
      <td>Alabama</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Anchorage</td>
      <td>Cities</td>
      <td>299455</td>
      <td>Alaska</td>
      <td>2</td>
      <td>3</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>8</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#output of combining csv, json and .db files
final_data.to_csv('question1.csv', index=False)
```


```python
#create a variable for a dataframe that will have an additional column that will contain the addition of the crimes
final_data_total = final_data
```


```python
#create a column to hold the addition of the crimes
final_data_total['Final_Total'] = final_data['quarter_1'] + final_data['quarter_2'] + final_data['quarter_3'] + final_data['quarter_4']
```


```python
#get the sum of the crimes
final_data_total['Final_Total'].sum()
```




    5869




```python
#create and display dataframe that groups data by Agency_name and crime in each quarter
data_question_two_a = final_data_total.groupby(['Agency_name'])[['quarter_1', 'quarter_2', 'quarter_3', 'quarter_4']].sum()
data_question_two_a
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>quarter_1</th>
      <th>quarter_2</th>
      <th>quarter_3</th>
      <th>quarter_4</th>
    </tr>
    <tr>
      <th>Agency_name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aberdeen</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Aberdeen Township</th>
      <td>1</td>
      <td>6</td>
      <td>1</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Acton</th>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Ada</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Adams</th>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Adelanto</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Adrian</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Agoura Hills</th>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Akron</th>
      <td>3</td>
      <td>3</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Alachua</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Alameda</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Albany</th>
      <td>0</td>
      <td>2</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Albemarle</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Albemarle County Police Department</th>
      <td>1</td>
      <td>5</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Albion</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Albuquerque</th>
      <td>2</td>
      <td>1</td>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Algoma</th>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Alhambra</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Allenhurst</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Alliance</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Alpena</th>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Alpine</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Altoona</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Altus</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Amador</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Amarillo College</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Ames</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Amesbury</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Amherst</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Amherst Town</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Windham</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Windsor Locks</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Winnsboro</th>
      <td>2</td>
      <td>3</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Wiscasset</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Wolcott</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Woodbridge Township</th>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Woodbury</th>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Woodbury Heights</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Woodhaven</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Woods Cross</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Woodstock</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Woolwich Township</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Wooster</th>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Worcester</th>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Wrightsville Beach</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Wyandotte</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Wyoming</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Xenia</th>
      <td>1</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Yakima</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Yale University</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Yamhill</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Yonkers</th>
      <td>2</td>
      <td>0</td>
      <td>3</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Yorba Linda</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>York</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Youngstown</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Yuba</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Yuba City</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Yucca Valley</th>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Yuma</th>
      <td>3</td>
      <td>6</td>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Zanesville</th>
      <td>1</td>
      <td>2</td>
      <td>0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>1572 rows × 4 columns</p>
</div>




```python
#display % of crimes committed per quarter by Agency and output to csv
data_question_two_a_percent = data_question_two_a/final_data['Final_Total'].sum()*100
data_question_two_a_percent
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>quarter_1</th>
      <th>quarter_2</th>
      <th>quarter_3</th>
      <th>quarter_4</th>
    </tr>
    <tr>
      <th>Agency_name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Aberdeen</th>
      <td>0.017039</td>
      <td>0.017039</td>
      <td>0.017039</td>
      <td>0.051116</td>
    </tr>
    <tr>
      <th>Aberdeen Township</th>
      <td>0.017039</td>
      <td>0.102232</td>
      <td>0.017039</td>
      <td>0.051116</td>
    </tr>
    <tr>
      <th>Acton</th>
      <td>0.000000</td>
      <td>0.034077</td>
      <td>0.000000</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>Ada</th>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>Adams</th>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.034077</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Adelanto</th>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Adrian</th>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Agoura Hills</th>
      <td>0.000000</td>
      <td>0.034077</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Akron</th>
      <td>0.051116</td>
      <td>0.051116</td>
      <td>0.034077</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Alachua</th>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Alameda</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>Albany</th>
      <td>0.000000</td>
      <td>0.034077</td>
      <td>0.017039</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Albemarle</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>Albemarle County Police Department</th>
      <td>0.017039</td>
      <td>0.085193</td>
      <td>0.034077</td>
      <td>0.034077</td>
    </tr>
    <tr>
      <th>Albion</th>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Albuquerque</th>
      <td>0.034077</td>
      <td>0.017039</td>
      <td>0.102232</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>Algoma</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.034077</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Alhambra</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>Allenhurst</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>Alliance</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Alpena</th>
      <td>0.034077</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Alpine</th>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Altoona</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Altus</th>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Amador</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Amarillo College</th>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Ames</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>Amesbury</th>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Amherst</th>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Amherst Town</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.034077</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Windham</th>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Windsor Locks</th>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Winnsboro</th>
      <td>0.034077</td>
      <td>0.051116</td>
      <td>0.000000</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>Wiscasset</th>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Wolcott</th>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Woodbridge Township</th>
      <td>0.000000</td>
      <td>0.034077</td>
      <td>0.000000</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>Woodbury</th>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.034077</td>
      <td>0.051116</td>
    </tr>
    <tr>
      <th>Woodbury Heights</th>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Woodhaven</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>Woods Cross</th>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>Woodstock</th>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Woolwich Township</th>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Wooster</th>
      <td>0.017039</td>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Worcester</th>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.017039</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Wrightsville Beach</th>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Wyandotte</th>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Wyoming</th>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>Xenia</th>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>Yakima</th>
      <td>0.017039</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.034077</td>
    </tr>
    <tr>
      <th>Yale University</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>Yamhill</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>Yonkers</th>
      <td>0.034077</td>
      <td>0.000000</td>
      <td>0.051116</td>
      <td>0.034077</td>
    </tr>
    <tr>
      <th>Yorba Linda</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
    </tr>
    <tr>
      <th>York</th>
      <td>0.017039</td>
      <td>0.017039</td>
      <td>0.017039</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Youngstown</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Yuba</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Yuba City</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Yucca Valley</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.017039</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>Yuma</th>
      <td>0.051116</td>
      <td>0.102232</td>
      <td>0.000000</td>
      <td>0.051116</td>
    </tr>
    <tr>
      <th>Zanesville</th>
      <td>0.017039</td>
      <td>0.034077</td>
      <td>0.000000</td>
      <td>0.017039</td>
    </tr>
  </tbody>
</table>
<p>1572 rows × 4 columns</p>
</div>




```python
#output % of crimes committed per quarter by Agency and output to csv
data_question_two_a_percent.to_csv('question2a.csv', index=False)
```


```python
#show agency reporting maximum number of crime
data_question_two_b = final_data_total.groupby(['Agency_type'])['Final_Total'].max()
data_question_two_b
```




    Agency_type
    Cities                       314
    Metropolitan Counties         87
    Nonmetropolitan Counties       5
    Other Agencies                17
    State Police Agencies          7
    Universities and Colleges      8
    Name: Final_Total, dtype: int64




```python
#States having the most crimes committed against the most ehtnic group
data_question_three = final_data_total.groupby(['State', 'Ethnicity'])['Final_Total'].max()
data_question_three
```




    State          Ethnicity
    Alabama        0              2
    Alaska         0              8
    Arizona        0              3
                   1             26
                   3             10
                   14            81
    Arkansas       0              4
                   1              3
    California     0             13
                   1             43
                   2             16
                   3              9
                   4              7
                   9            114
                   10            50
    Colorado       0              8
                   1             30
                   2              2
    Connecticut    0              6
                   1             10
                   2              8
                   3             11
                   6              7
    DC             1              2
                   3             70
    Delaware       0              2
    Florida        0             10
                   1              3
                   2              2
    Georgia        0              4
                               ... 
    Tennessee      0              5
                   1             24
                   2              5
                   4              6
                   6             11
                   12            17
                   36            46
    Texas          0              3
                   1             11
                   2              4
                   3              4
                   4             18
                   5             16
    Utah           0              5
                   1              5
                   3              6
    Vermont        0              3
    Virginia       0              7
                   1             13
    Washington     0             11
                   1             13
                   2             10
                   3             10
                   6             89
    West_Virginia  0             14
                   1              8
    Wisconsin      0              9
                   1              2
                   5             12
    Wyoming        1              1
    Name: Final_Total, dtype: int64




```python
#display total number of crimes committed on the basis of disability
data_question_four = final_data_total.groupby(['Disability'])['Final_Total'].sum()
data_question_four
```




    Disability
    0     4818
    1      769
    2       35
    3       94
    4       17
    12     136
    Name: Final_Total, dtype: int64




```python
#display % of crime committed on the basis of disability
data_question_four/final_data['Final_Total'].sum()*100
```




    Disability
    0     82.092350
    1     13.102743
    2      0.596354
    3      1.601636
    4      0.289658
    12     2.317260
    Name: Final_Total, dtype: float64


