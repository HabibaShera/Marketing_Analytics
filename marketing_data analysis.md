```python
from numpy import *
from pandas import * 
import seaborn as sns
import matplotlib.pyplot as plt
set_option('display.max_columns',None)
import datetime as dt
```


```python
data=read_csv('marketing_data.csv')
data.head()
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
      <th>ID</th>
      <th>Year_Birth</th>
      <th>Education</th>
      <th>Marital_Status</th>
      <th>Income</th>
      <th>Kidhome</th>
      <th>Teenhome</th>
      <th>Dt_Customer</th>
      <th>Recency</th>
      <th>MntWines</th>
      <th>MntFruits</th>
      <th>MntMeatProducts</th>
      <th>MntFishProducts</th>
      <th>MntSweetProducts</th>
      <th>MntGoldProds</th>
      <th>NumDealsPurchases</th>
      <th>NumWebPurchases</th>
      <th>NumCatalogPurchases</th>
      <th>NumStorePurchases</th>
      <th>NumWebVisitsMonth</th>
      <th>AcceptedCmp3</th>
      <th>AcceptedCmp4</th>
      <th>AcceptedCmp5</th>
      <th>AcceptedCmp1</th>
      <th>AcceptedCmp2</th>
      <th>Response</th>
      <th>Complain</th>
      <th>Country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1826</td>
      <td>1970</td>
      <td>Graduation</td>
      <td>Divorced</td>
      <td>$84,835.00</td>
      <td>0</td>
      <td>0</td>
      <td>6/16/14</td>
      <td>0</td>
      <td>189</td>
      <td>104</td>
      <td>379</td>
      <td>111</td>
      <td>189</td>
      <td>218</td>
      <td>1</td>
      <td>4</td>
      <td>4</td>
      <td>6</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1961</td>
      <td>Graduation</td>
      <td>Single</td>
      <td>$57,091.00</td>
      <td>0</td>
      <td>0</td>
      <td>6/15/14</td>
      <td>0</td>
      <td>464</td>
      <td>5</td>
      <td>64</td>
      <td>7</td>
      <td>0</td>
      <td>37</td>
      <td>1</td>
      <td>7</td>
      <td>3</td>
      <td>7</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10476</td>
      <td>1958</td>
      <td>Graduation</td>
      <td>Married</td>
      <td>$67,267.00</td>
      <td>0</td>
      <td>1</td>
      <td>5/13/14</td>
      <td>0</td>
      <td>134</td>
      <td>11</td>
      <td>59</td>
      <td>15</td>
      <td>2</td>
      <td>30</td>
      <td>1</td>
      <td>3</td>
      <td>2</td>
      <td>5</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>US</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1386</td>
      <td>1967</td>
      <td>Graduation</td>
      <td>Together</td>
      <td>$32,474.00</td>
      <td>1</td>
      <td>1</td>
      <td>5/11/14</td>
      <td>0</td>
      <td>10</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>AUS</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5371</td>
      <td>1989</td>
      <td>Graduation</td>
      <td>Single</td>
      <td>$21,474.00</td>
      <td>1</td>
      <td>0</td>
      <td>4/8/14</td>
      <td>0</td>
      <td>6</td>
      <td>16</td>
      <td>24</td>
      <td>11</td>
      <td>0</td>
      <td>34</td>
      <td>2</td>
      <td>3</td>
      <td>1</td>
      <td>2</td>
      <td>7</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>SP</td>
    </tr>
  </tbody>
</table>
</div>




```python
data.columns=data.columns.str.lower()
data.columns
```




    Index(['id', 'year_birth', 'education', 'marital_status', ' income ',
           'kidhome', 'teenhome', 'dt_customer', 'recency', 'mntwines',
           'mntfruits', 'mntmeatproducts', 'mntfishproducts', 'mntsweetproducts',
           'mntgoldprods', 'numdealspurchases', 'numwebpurchases',
           'numcatalogpurchases', 'numstorepurchases', 'numwebvisitsmonth',
           'acceptedcmp3', 'acceptedcmp4', 'acceptedcmp5', 'acceptedcmp1',
           'acceptedcmp2', 'response', 'complain', 'country'],
          dtype='object')




```python
data.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 2240 entries, 0 to 2239
    Data columns (total 28 columns):
     #   Column               Non-Null Count  Dtype 
    ---  ------               --------------  ----- 
     0   id                   2240 non-null   int64 
     1   year_birth           2240 non-null   int64 
     2   education            2240 non-null   object
     3   marital_status       2240 non-null   object
     4    income              2216 non-null   object
     5   kidhome              2240 non-null   int64 
     6   teenhome             2240 non-null   int64 
     7   dt_customer          2240 non-null   object
     8   recency              2240 non-null   int64 
     9   mntwines             2240 non-null   int64 
     10  mntfruits            2240 non-null   int64 
     11  mntmeatproducts      2240 non-null   int64 
     12  mntfishproducts      2240 non-null   int64 
     13  mntsweetproducts     2240 non-null   int64 
     14  mntgoldprods         2240 non-null   int64 
     15  numdealspurchases    2240 non-null   int64 
     16  numwebpurchases      2240 non-null   int64 
     17  numcatalogpurchases  2240 non-null   int64 
     18  numstorepurchases    2240 non-null   int64 
     19  numwebvisitsmonth    2240 non-null   int64 
     20  acceptedcmp3         2240 non-null   int64 
     21  acceptedcmp4         2240 non-null   int64 
     22  acceptedcmp5         2240 non-null   int64 
     23  acceptedcmp1         2240 non-null   int64 
     24  acceptedcmp2         2240 non-null   int64 
     25  response             2240 non-null   int64 
     26  complain             2240 non-null   int64 
     27  country              2240 non-null   object
    dtypes: int64(23), object(5)
    memory usage: 446.3+ KB
    

#          

# Data Cleaning


```python
data.columns=data.columns.str.strip()
data.columns
```




    Index(['id', 'year_birth', 'education', 'marital_status', 'income', 'kidhome',
           'teenhome', 'dt_customer', 'recency', 'mntwines', 'mntfruits',
           'mntmeatproducts', 'mntfishproducts', 'mntsweetproducts',
           'mntgoldprods', 'numdealspurchases', 'numwebpurchases',
           'numcatalogpurchases', 'numstorepurchases', 'numwebvisitsmonth',
           'acceptedcmp3', 'acceptedcmp4', 'acceptedcmp5', 'acceptedcmp1',
           'acceptedcmp2', 'response', 'complain', 'country'],
          dtype='object')




```python
#we observe that income column is in object format, so we need to transform it to int64 or float
data['income']=data['income'].str.strip('$')
data['income']=data['income'].str.replace(',','')
data['income']=to_numeric(data['income'],errors='coerce')
data['income'].dtypes
```




    dtype('float64')




```python
data['income'].dtypes
```




    dtype('float64')




```python
data.isnull().sum().sort_values(ascending=False)[:4]
```




    income        24
    country        0
    complain       0
    year_birth     0
    dtype: int64




```python
f=plt.figure(figsize=(20,8))
ax=f.add_subplot(121)
sns.boxplot(data=data,x='income',ax=ax)
ax.set_title('Show Outlies')

ax=f.add_subplot(122)
data.hist('income',ax=ax)
ax.set_title('Income Distribution')
```




    Text(0.5, 1.0, 'Income Distribution')




![png](output_10_1.png)



```python
#From these plots we can observe that there are outliers in this column, so the way to refill the missing values is median
data.fillna({'income':data['income'].median()},inplace=True)
```


```python
data.isnull().sum().sort_values(ascending=False)[:2]
```




    country     0
    complain    0
    dtype: int64




```python
# To make dt_customer more readable, we can do this:
data['dt_customer']=to_datetime(data['dt_customer'])
data.head()
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
      <th>year_birth</th>
      <th>education</th>
      <th>marital_status</th>
      <th>income</th>
      <th>kidhome</th>
      <th>teenhome</th>
      <th>dt_customer</th>
      <th>recency</th>
      <th>mntwines</th>
      <th>mntfruits</th>
      <th>mntmeatproducts</th>
      <th>mntfishproducts</th>
      <th>mntsweetproducts</th>
      <th>mntgoldprods</th>
      <th>numdealspurchases</th>
      <th>numwebpurchases</th>
      <th>numcatalogpurchases</th>
      <th>numstorepurchases</th>
      <th>numwebvisitsmonth</th>
      <th>acceptedcmp3</th>
      <th>acceptedcmp4</th>
      <th>acceptedcmp5</th>
      <th>acceptedcmp1</th>
      <th>acceptedcmp2</th>
      <th>response</th>
      <th>complain</th>
      <th>country</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1826</td>
      <td>1970</td>
      <td>Graduation</td>
      <td>Divorced</td>
      <td>84835.0</td>
      <td>0</td>
      <td>0</td>
      <td>2014-06-16</td>
      <td>0</td>
      <td>189</td>
      <td>104</td>
      <td>379</td>
      <td>111</td>
      <td>189</td>
      <td>218</td>
      <td>1</td>
      <td>4</td>
      <td>4</td>
      <td>6</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>SP</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1961</td>
      <td>Graduation</td>
      <td>Single</td>
      <td>57091.0</td>
      <td>0</td>
      <td>0</td>
      <td>2014-06-15</td>
      <td>0</td>
      <td>464</td>
      <td>5</td>
      <td>64</td>
      <td>7</td>
      <td>0</td>
      <td>37</td>
      <td>1</td>
      <td>7</td>
      <td>3</td>
      <td>7</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>CA</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10476</td>
      <td>1958</td>
      <td>Graduation</td>
      <td>Married</td>
      <td>67267.0</td>
      <td>0</td>
      <td>1</td>
      <td>2014-05-13</td>
      <td>0</td>
      <td>134</td>
      <td>11</td>
      <td>59</td>
      <td>15</td>
      <td>2</td>
      <td>30</td>
      <td>1</td>
      <td>3</td>
      <td>2</td>
      <td>5</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>US</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1386</td>
      <td>1967</td>
      <td>Graduation</td>
      <td>Together</td>
      <td>32474.0</td>
      <td>1</td>
      <td>1</td>
      <td>2014-05-11</td>
      <td>0</td>
      <td>10</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>AUS</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5371</td>
      <td>1989</td>
      <td>Graduation</td>
      <td>Single</td>
      <td>21474.0</td>
      <td>1</td>
      <td>0</td>
      <td>2014-04-08</td>
      <td>0</td>
      <td>6</td>
      <td>16</td>
      <td>24</td>
      <td>11</td>
      <td>0</td>
      <td>34</td>
      <td>2</td>
      <td>3</td>
      <td>1</td>
      <td>2</td>
      <td>7</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>SP</td>
    </tr>
  </tbody>
</table>
</div>



#            

# Data Exploration


```python
data['marital_status'].value_counts()
```




    Married     864
    Together    580
    Single      480
    Divorced    232
    Widow        77
    Alone         3
    Absurd        2
    YOLO          2
    Name: marital_status, dtype: int64




```python
plt.figure(figsize=(8,5))
sns.countplot(x='marital_status',data=data)
plt.title('Marital Status Counts')
```




    Text(0.5, 1.0, 'Marital Status Counts')




![png](output_17_1.png)


### from this plot, we can note that:
- The most popular in data is married
- The second most popular in data is together and single

#                      


```python
plt.figure(figsize=(10,7))
edu=data['education'].value_counts()
plt.pie(edu.values,labels=edu.index,autopct='%1.f%%')
plt.title('Education Distribution');
```


![png](output_20_0.png)


### Notes of this plot:
- The most popular education in data is graduation
- A few people who have basic education and 2n cycle

#        


```python
data['age']=dt.date.today().year-data['year_birth']
data.head()
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
      <th>year_birth</th>
      <th>education</th>
      <th>marital_status</th>
      <th>income</th>
      <th>kidhome</th>
      <th>teenhome</th>
      <th>dt_customer</th>
      <th>recency</th>
      <th>mntwines</th>
      <th>mntfruits</th>
      <th>mntmeatproducts</th>
      <th>mntfishproducts</th>
      <th>mntsweetproducts</th>
      <th>mntgoldprods</th>
      <th>numdealspurchases</th>
      <th>numwebpurchases</th>
      <th>numcatalogpurchases</th>
      <th>numstorepurchases</th>
      <th>numwebvisitsmonth</th>
      <th>acceptedcmp3</th>
      <th>acceptedcmp4</th>
      <th>acceptedcmp5</th>
      <th>acceptedcmp1</th>
      <th>acceptedcmp2</th>
      <th>response</th>
      <th>complain</th>
      <th>country</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1826</td>
      <td>1970</td>
      <td>Graduation</td>
      <td>Divorced</td>
      <td>84835.0</td>
      <td>0</td>
      <td>0</td>
      <td>2014-06-16</td>
      <td>0</td>
      <td>189</td>
      <td>104</td>
      <td>379</td>
      <td>111</td>
      <td>189</td>
      <td>218</td>
      <td>1</td>
      <td>4</td>
      <td>4</td>
      <td>6</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>SP</td>
      <td>51</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1961</td>
      <td>Graduation</td>
      <td>Single</td>
      <td>57091.0</td>
      <td>0</td>
      <td>0</td>
      <td>2014-06-15</td>
      <td>0</td>
      <td>464</td>
      <td>5</td>
      <td>64</td>
      <td>7</td>
      <td>0</td>
      <td>37</td>
      <td>1</td>
      <td>7</td>
      <td>3</td>
      <td>7</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>CA</td>
      <td>60</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10476</td>
      <td>1958</td>
      <td>Graduation</td>
      <td>Married</td>
      <td>67267.0</td>
      <td>0</td>
      <td>1</td>
      <td>2014-05-13</td>
      <td>0</td>
      <td>134</td>
      <td>11</td>
      <td>59</td>
      <td>15</td>
      <td>2</td>
      <td>30</td>
      <td>1</td>
      <td>3</td>
      <td>2</td>
      <td>5</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>US</td>
      <td>63</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1386</td>
      <td>1967</td>
      <td>Graduation</td>
      <td>Together</td>
      <td>32474.0</td>
      <td>1</td>
      <td>1</td>
      <td>2014-05-11</td>
      <td>0</td>
      <td>10</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>AUS</td>
      <td>54</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5371</td>
      <td>1989</td>
      <td>Graduation</td>
      <td>Single</td>
      <td>21474.0</td>
      <td>1</td>
      <td>0</td>
      <td>2014-04-08</td>
      <td>0</td>
      <td>6</td>
      <td>16</td>
      <td>24</td>
      <td>11</td>
      <td>0</td>
      <td>34</td>
      <td>2</td>
      <td>3</td>
      <td>1</td>
      <td>2</td>
      <td>7</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>SP</td>
      <td>32</td>
    </tr>
  </tbody>
</table>
</div>




```python
data['age'].describe()
```




    count    2240.000000
    mean       52.194196
    std        11.984069
    min        25.000000
    25%        44.000000
    50%        51.000000
    75%        62.000000
    max       128.000000
    Name: age, dtype: float64




```python
plt.figure(figsize=(12,5))
sns.histplot(data=data,x='age')
plt.title('Ages Distribution')
```




    Text(0.5, 1.0, 'Ages Distribution')




![png](output_25_1.png)


- Most ages are between 44 and 62

#          


```python
plt.figure(figsize=(10,7))
count=data['kidhome'].value_counts()
plt.pie(count.values,labels=count.index,autopct='%1.0f%%');
plt.title("Distribution of kids in Customers'home")
```




    Text(0.5, 1.0, "Distribution of kids in Customers'home")




![png](output_28_1.png)


- Most customers have no children in their homes.
- 40% of them have one child in their home.

#        


```python
plt.figure(figsize=(12,8))
counts=data['teenhome'].value_counts()
plt.pie(counts.values,labels=counts.index,autopct='%1.0f%%');
plt.title('Teenegers Distribution')
```




    Text(0.5, 1.0, 'Teenegers Distribution')




![png](output_31_1.png)


- Most customers have no teenagers in their homes.
- 46% of customers have one teenager in their homes.

#      


```python
data['month_customer']=data['dt_customer'].dt.month
data.head()
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
      <th>year_birth</th>
      <th>education</th>
      <th>marital_status</th>
      <th>income</th>
      <th>kidhome</th>
      <th>teenhome</th>
      <th>dt_customer</th>
      <th>recency</th>
      <th>mntwines</th>
      <th>mntfruits</th>
      <th>mntmeatproducts</th>
      <th>mntfishproducts</th>
      <th>mntsweetproducts</th>
      <th>mntgoldprods</th>
      <th>numdealspurchases</th>
      <th>numwebpurchases</th>
      <th>numcatalogpurchases</th>
      <th>numstorepurchases</th>
      <th>numwebvisitsmonth</th>
      <th>acceptedcmp3</th>
      <th>acceptedcmp4</th>
      <th>acceptedcmp5</th>
      <th>acceptedcmp1</th>
      <th>acceptedcmp2</th>
      <th>response</th>
      <th>complain</th>
      <th>country</th>
      <th>age</th>
      <th>month_customer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1826</td>
      <td>1970</td>
      <td>Graduation</td>
      <td>Divorced</td>
      <td>84835.0</td>
      <td>0</td>
      <td>0</td>
      <td>2014-06-16</td>
      <td>0</td>
      <td>189</td>
      <td>104</td>
      <td>379</td>
      <td>111</td>
      <td>189</td>
      <td>218</td>
      <td>1</td>
      <td>4</td>
      <td>4</td>
      <td>6</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>SP</td>
      <td>51</td>
      <td>6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1961</td>
      <td>Graduation</td>
      <td>Single</td>
      <td>57091.0</td>
      <td>0</td>
      <td>0</td>
      <td>2014-06-15</td>
      <td>0</td>
      <td>464</td>
      <td>5</td>
      <td>64</td>
      <td>7</td>
      <td>0</td>
      <td>37</td>
      <td>1</td>
      <td>7</td>
      <td>3</td>
      <td>7</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>CA</td>
      <td>60</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10476</td>
      <td>1958</td>
      <td>Graduation</td>
      <td>Married</td>
      <td>67267.0</td>
      <td>0</td>
      <td>1</td>
      <td>2014-05-13</td>
      <td>0</td>
      <td>134</td>
      <td>11</td>
      <td>59</td>
      <td>15</td>
      <td>2</td>
      <td>30</td>
      <td>1</td>
      <td>3</td>
      <td>2</td>
      <td>5</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>US</td>
      <td>63</td>
      <td>5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1386</td>
      <td>1967</td>
      <td>Graduation</td>
      <td>Together</td>
      <td>32474.0</td>
      <td>1</td>
      <td>1</td>
      <td>2014-05-11</td>
      <td>0</td>
      <td>10</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>AUS</td>
      <td>54</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5371</td>
      <td>1989</td>
      <td>Graduation</td>
      <td>Single</td>
      <td>21474.0</td>
      <td>1</td>
      <td>0</td>
      <td>2014-04-08</td>
      <td>0</td>
      <td>6</td>
      <td>16</td>
      <td>24</td>
      <td>11</td>
      <td>0</td>
      <td>34</td>
      <td>2</td>
      <td>3</td>
      <td>1</td>
      <td>2</td>
      <td>7</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>SP</td>
      <td>32</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
data['year_customer']=data['dt_customer'].dt.year
data.head()
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
      <th>year_birth</th>
      <th>education</th>
      <th>marital_status</th>
      <th>income</th>
      <th>kidhome</th>
      <th>teenhome</th>
      <th>dt_customer</th>
      <th>recency</th>
      <th>mntwines</th>
      <th>mntfruits</th>
      <th>mntmeatproducts</th>
      <th>mntfishproducts</th>
      <th>mntsweetproducts</th>
      <th>mntgoldprods</th>
      <th>numdealspurchases</th>
      <th>numwebpurchases</th>
      <th>numcatalogpurchases</th>
      <th>numstorepurchases</th>
      <th>numwebvisitsmonth</th>
      <th>acceptedcmp3</th>
      <th>acceptedcmp4</th>
      <th>acceptedcmp5</th>
      <th>acceptedcmp1</th>
      <th>acceptedcmp2</th>
      <th>response</th>
      <th>complain</th>
      <th>country</th>
      <th>age</th>
      <th>month_customer</th>
      <th>year_customer</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1826</td>
      <td>1970</td>
      <td>Graduation</td>
      <td>Divorced</td>
      <td>84835.0</td>
      <td>0</td>
      <td>0</td>
      <td>2014-06-16</td>
      <td>0</td>
      <td>189</td>
      <td>104</td>
      <td>379</td>
      <td>111</td>
      <td>189</td>
      <td>218</td>
      <td>1</td>
      <td>4</td>
      <td>4</td>
      <td>6</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>SP</td>
      <td>51</td>
      <td>6</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>1961</td>
      <td>Graduation</td>
      <td>Single</td>
      <td>57091.0</td>
      <td>0</td>
      <td>0</td>
      <td>2014-06-15</td>
      <td>0</td>
      <td>464</td>
      <td>5</td>
      <td>64</td>
      <td>7</td>
      <td>0</td>
      <td>37</td>
      <td>1</td>
      <td>7</td>
      <td>3</td>
      <td>7</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>CA</td>
      <td>60</td>
      <td>6</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10476</td>
      <td>1958</td>
      <td>Graduation</td>
      <td>Married</td>
      <td>67267.0</td>
      <td>0</td>
      <td>1</td>
      <td>2014-05-13</td>
      <td>0</td>
      <td>134</td>
      <td>11</td>
      <td>59</td>
      <td>15</td>
      <td>2</td>
      <td>30</td>
      <td>1</td>
      <td>3</td>
      <td>2</td>
      <td>5</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>US</td>
      <td>63</td>
      <td>5</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1386</td>
      <td>1967</td>
      <td>Graduation</td>
      <td>Together</td>
      <td>32474.0</td>
      <td>1</td>
      <td>1</td>
      <td>2014-05-11</td>
      <td>0</td>
      <td>10</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>7</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>AUS</td>
      <td>54</td>
      <td>5</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5371</td>
      <td>1989</td>
      <td>Graduation</td>
      <td>Single</td>
      <td>21474.0</td>
      <td>1</td>
      <td>0</td>
      <td>2014-04-08</td>
      <td>0</td>
      <td>6</td>
      <td>16</td>
      <td>24</td>
      <td>11</td>
      <td>0</td>
      <td>34</td>
      <td>2</td>
      <td>3</td>
      <td>1</td>
      <td>2</td>
      <td>7</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>SP</td>
      <td>32</td>
      <td>4</td>
      <td>2014</td>
    </tr>
  </tbody>
</table>
</div>




```python
#function to show the precentage of each column in the plot
def show_percent(col):
    plt.figure(figsize=(20,12))
    ax=sns.countplot(data=data,x=col)
    plt.xticks(rotation=90)
    plt.title(f'{col} Distribution')
    
    total=float(len(data))
    for p in ax.patches:
        height=p.get_height()
        percent=(height*100)/total
        ax.text(p.get_x()+p.get_width()/2,height+1,'{:.0f}%'.format(percent),ha='center',weight='bold',fontsize=20)
```


```python
f=plt.figure(figsize=(15,9))
sns.catplot(data=data,x='year_customer',kind='count')
plt.title("Distribution Customer Registration Dates")
```




    Text(0.5, 1, 'Distribution Customer Registration Dates')




    <Figure size 1080x648 with 0 Axes>



![png](output_37_2.png)



```python
plt.figure(figsize=(10,7))
count=data['year_customer'].value_counts()
plt.pie(count.values,labels=count.index,autopct='%1.0f%%');
plt.title("Distribution Customer Registration Dates")
```




    Text(0.5, 1.0, 'Distribution Customer Registration Dates')




![png](output_38_1.png)



```python
show_percent('year_customer')
```


![png](output_39_0.png)


### From this plot, we note that:
- Most customers' registration was in 2013. After that, The number of registration is decreasing

#        


```python
sns.countplot(data=data,x='month_customer')
```




    <matplotlib.axes._subplots.AxesSubplot at 0xaf1aa90>




![png](output_42_1.png)



```python
show_percent('month_customer')
```


![png](output_43_0.png)


- On last 3 years, The registration is fine.
- In July, The numbers of registration decreased.

#           


```python
registration_2012=data[data['year_customer']==2012].month_customer
registration_2013=data[data['year_customer']==2013].month_customer
registration_2014=data[data['year_customer']==2014].month_customer
```


```python
f=plt.figure(figsize=(20,5))
ax=f.add_subplot(131)
sns.countplot(x=registration_2012,data=data,ax=ax)
ax.set_title("The Registration's Numbers in 2012")

ax=f.add_subplot(132)
sns.countplot(x=registration_2013,data=data,ax=ax)
ax.set_title("The Registration's Numbers in 2013")

ax=f.add_subplot(133)
sns.countplot(x=registration_2014,data=data,ax=ax)
ax.set_title("The Registration's Numbers in 2014")
```




    Text(0.5, 1.0, "The Registration's Numbers in 2014")




![png](output_47_1.png)


- We should remember the data is from July 2012 to June 2014 so, everything is good in the number of registration.

#   


```python
products=['mntwines','mntfruits','mntmeatproducts','mntfishproducts','mntsweetproducts','mntgoldprods']
data[products].sum().sort_values()
```




    mntfruits            58917
    mntsweetproducts     60621
    mntfishproducts      84057
    mntgoldprods         98609
    mntmeatproducts     373968
    mntwines            680816
    dtype: int64




```python
f=plt.figure(figsize=(20,13))
for i,col in enumerate(products):
    ax=f.add_subplot(2,3,i+1)
    sns.histplot(data=data,x=col,ax=ax)
    ax.set_title(f"{col.replace('mnt','').title()} Distribution")
```


![png](output_51_0.png)


- Most customers spend their money on wines.
- The arrange of money spent are with descending:
    - wines
    - meat
    - gold
    - fish
    - sweet
    - fruits

#       


```python
data[products].describe()
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
      <th>mntwines</th>
      <th>mntfruits</th>
      <th>mntmeatproducts</th>
      <th>mntfishproducts</th>
      <th>mntsweetproducts</th>
      <th>mntgoldprods</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>2240.000000</td>
      <td>2240.000000</td>
      <td>2240.000000</td>
      <td>2240.000000</td>
      <td>2240.000000</td>
      <td>2240.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>303.935714</td>
      <td>26.302232</td>
      <td>166.950000</td>
      <td>37.525446</td>
      <td>27.062946</td>
      <td>44.021875</td>
    </tr>
    <tr>
      <th>std</th>
      <td>336.597393</td>
      <td>39.773434</td>
      <td>225.715373</td>
      <td>54.628979</td>
      <td>41.280498</td>
      <td>52.167439</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>23.750000</td>
      <td>1.000000</td>
      <td>16.000000</td>
      <td>3.000000</td>
      <td>1.000000</td>
      <td>9.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>173.500000</td>
      <td>8.000000</td>
      <td>67.000000</td>
      <td>12.000000</td>
      <td>8.000000</td>
      <td>24.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>504.250000</td>
      <td>33.000000</td>
      <td>232.000000</td>
      <td>50.000000</td>
      <td>33.000000</td>
      <td>56.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1493.000000</td>
      <td>199.000000</td>
      <td>1725.000000</td>
      <td>259.000000</td>
      <td>263.000000</td>
      <td>362.000000</td>
    </tr>
  </tbody>
</table>
</div>



### The conclusion of this table is:
- The maxium price is for meat products (1725)
- After that, wines products are (1493)


### The range of some products:
_Wines_ :
    - Most customer spent on wines from 23 to 504
_Fruits_ :
    - Most customer spent on fruits from 1 to 33
_Meats_ :
    - Most customer spent on meats from 16 to 232
_Fishes_ :
    - Most customer spent on fishes from 3 to 50
_Sweets_ :
    - Most customer spent on sweets from 1 to 33
_Gold_ :
    - Most customer spent on gold from 9 to 56

#         


```python
len(data[data['mntgoldprods']==0].mntgoldprods)
```




    61




```python
sum_0_values=[]
for i in products:
    sum_0_values.append(len(data[data[i]==0]))
```


```python
sum_0_values
```




    [13, 400, 1, 384, 419, 61]




```python
plt.figure(figsize=(12,8))
plt.pie(x=sum_0_values,labels=products,autopct='%1.0f%%');
```


![png](output_60_0.png)



```python
plt.figure(figsize=(8,5))
sns.barplot(x=products,y=sum_0_values,order=['mntsweetproducts','mntfruits','mntfishproducts','mntgoldprods','mntwines','mntmeatproducts'])
plt.xticks(rotation=90)
plt.xlabel('Products')
plt.ylabel('Counts')
plt.title('Distribution Of Products Customers Do Not Buy')
```




    Text(0.5, 1.0, 'Distribution Of Products Customers Do Not Buy')




![png](output_61_1.png)


### From this plots, we note that:
- The most products customers buy is:
    - meat
    - wines
    - gold

#          


```python
accept=['acceptedcmp1','acceptedcmp2','acceptedcmp3','acceptedcmp4','acceptedcmp5']
#number of customer accept the camp
accept_num=[]

#number of customer don't accept the camp
not_accept_num=[]

for i in accept:
    accept_num.append(len(data[data[i]==1]))
    not_accept_num.append(len(data[data[i]==0]))
```


```python
accept_num
```




    [144, 30, 163, 167, 163]




```python
not_accept_num
```




    [2096, 2210, 2077, 2073, 2077]



#      


```python
sns.set_context('talk')
f=plt.figure(figsize=(20,8))
ax=f.add_subplot(121)
sns.barplot(x=accept,y=accept_num,ax=ax)
plt.xlabel('Camps')
plt.ylabel('Counts')
plt.xticks(rotation=90)
plt.title('Number of customers Accept The Camp')


ax=f.add_subplot(122)
sns.barplot(x=accept,y=not_accept_num,ax=ax)
plt.xlabel('Camps')
plt.ylabel('Counts')
plt.title('Number of customers Do Not Accept The Camp')
plt.xticks(rotation=90)
```




    (array([0, 1, 2, 3, 4]), <a list of 5 Text xticklabel objects>)




![png](output_68_1.png)


### Notes from these plots:
- Most customers don't accept the camp.
- The range of customers accept the camp are between 140 and 160
- In the second camp, we can observe that:
    - Most customers don't accept this camp (almost 30 customers only accepted)

#           


```python
data['income'].describe()
```




    count      2240.000000
    mean      52237.975446
    std       25037.955891
    min        1730.000000
    25%       35538.750000
    50%       51381.500000
    75%       68289.750000
    max      666666.000000
    Name: income, dtype: float64




```python
plt.figure(figsize=(12,5))
sns.histplot(data=data,x='income')
plt.title('Income Distribution')
```




    Text(0.5, 1.0, 'Income Distribution')




![png](output_72_1.png)


- The range of the income of the most customers is between 35000 and 68000

#        
