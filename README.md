# Python_CheatSheet

- [Python_CheatSheet](#python_cheatsheet)
  - [1. Dataframe Operations](#1-dataframe-operations)
  - [2. Basic Python Stuffs](#2-basic-python-stuffs)
  - [3. Visualization](#3-visualization)
  - [4. System (pip) and Modules](#4-system-pip-and-modules)

[comment]: <> (This is a comment, it will not be included:)

## 1. Dataframe Operations

<details>
<summary>Dataframe summary</summary>

  ```python

  def summarize_df(df_input):
      """
      Summarized and returns a pandas dataframe denoting the total number of NA/Duplicated values and the percentage of NA/Duplicated values in each column.
      The column names are noted on the index.
      
      Parameters
      ----------
      data: dataframe
      """
      print(df_input.info())
      columnList = df_input.columns.tolist()        
          
      # pandas series denoting features and the sum of their null values
      null_sum = df_input.isnull().sum()# instantiate columns for missing data
      Nullpercent = ( ((null_sum / len(df_input.index))).round(2) )
      
      # pandas series denoting features and the sum of their duplicate value
      nunique_sum = df_input.nunique(dropna = False)
      Duplicatepercent = ( 1 - ((nunique_sum / len(df_input.index))).round(2) )
      
      # concatenate along the columns to create the complete dataframe
      df_NA = pd.concat([null_sum, Nullpercent, nunique_sum, Duplicatepercent], axis=1, keys=['Number of NA', 'Percent NA','Number of Uniques', 'Percent Duplicate'])
      
      return df_NA

  ```

</details>

<details>
<summary>Dataframe Selection</summary>

```python
recipes_dfUse2 = recipes_dfUse[['counts_x','user_id','User_popularity']]
```
</details>

<details>
<summary>Load csv with header or not</summary>

```python
dfRaw = pd.read_csv('./HW1_Problem2.csv', header=None)
dfRaw = pd.read_csv('./HW1_Problem2.csv')
```
</details>

<details>
<summary>Series reset_index + drop the original one</summary>

```python
reset_index(inplace=True, drop=True)
```
</details>

<details>
<summary>How to check if a value is in the list in selection from pandas data frame?</summary>

```python
  favorites_df[(favorites_df['recipe_id'].isin(tempList))]
```

</details>

<details>
<summary>Count the frequency that a value occurs in a dataframe column</summary>

```python
  df.groupby('a').count()
```

</details>

<details>
<summary>Pandas How to filter a Series</summary>

```python
test = {
383:    3.000000,
663:    1.000000,
726:    1.000000,
737:    9.000000,
833:    8.166667
}

s = pd.Series(test)
s = s[s != 1]
s
Out[0]:
383    3.000000
737    9.000000
833    8.166667
dtype: float64
```

</details>

<details>
<summary>Convert given Pandas series into a dataframe with its index as another column on the dataframe</summary>

```python
  df = s.to_frame().reset_index()
```

</details>

<details>
<summary>Pandas: change data type of Series to String</summary>

```python
  df.id.apply(str)
```

</details>

<details>
<summary>Add column to dataframe with constant value</summary>

```python
  df['Name']='abc' 
  ##will add the new column and set all rows to that value
```

</details>

<details>
<summary>df time expression</summary>

  ```python  
  df['year'] = pd.to_datetime(df['year'], format='%Y-%m')
  
  ```

</details>

<details>
<summary>select a coulmn as new index column</summary>

  `set_index`

  ```python  
  dfUse = dfUse.set_index('time_index')
  
  ```

</details>

<details>
<summary>How to apply a function to two columns of Pandas dataframe</summary>

  ```python  
  In [49]: df
  Out[49]: 
            0         1
  0  1.000000  0.000000
  1 -0.494375  0.570994
  2  1.000000  0.000000
  3  1.876360 -0.229738
  4  1.000000  0.000000

  In [50]: def f(x):    
    ....:  return x[0] + x[1]  
    ....:  

  In [51]: df.apply(f, axis=1) #passes a Series object, row-wise
  Out[51]: 
  0    1.000000
  1    0.076619
  2    1.000000
  3    1.646622
  4    1.000000
  
  ```

</details>

<details>
<summary>Merge two columns in df</summary>

  `pd.merge`

  ```python  
  dftemp = pd.merge(df1, df2, left_index=True, right_index=True)
  
  ```

</details>

<details>
<summary>Series to DF</summary>

  `pd.DataFrame(series_input)`

</details>

## 2. Basic Python Stuffs

<details>
<summary>Def format (Def_格式)</summary>

  ```python
  def get_jsonparsed_data(url):
      """
      Receive the content of ``url``, parse it as JSON and return the object.

      Parameters
      ----------
      url : str

      Returns
      -------
      dict
      """
      response = urlopen(url, cafile=certifi.where())
      data = response.read().decode("utf-8")
      return json.loads(data)
  ```

</details>

<details>
<summary>Print format</summary>

  ```python
  #1. String + Number
  print('RSS: %.4f'% numberHere)

  ```

</details>

<details>
<summary>Scientific Expression</summary>

  ```python  
  rss = "{:.2e}".format(Numhere)
  
  ```

</details>


## 3. Visualization



<details>
<summary>Histogram</summary>

  ```python
  fig = plt.figure(figsize = (8, 4))
sns.histplot(data = recipes_df, 
            x = 'published_at',  kde = True,
            bins = 52, 
            legend = False
)
plt.title('# recipes over time')
# fig.savefig('/content/img/n_recipes_over_time.jpg')

  ```
![image](./img/histogram_template.png)
</details>


<details>
  <summary>Regular plt</summary>

  ```python
    fig = plt.figure()
    axes = plt.axes()
    axes.plot(x, y)
    axes.set_title('A simple plot')
    axes.set_xlabel('x')
    plt.show()
  ```

</details>

<details>
  <summary>for-loop subplots</summary>

  ```python

fig = plt.figure(figsize=(28,10))
fig.subplots_adjust(hspace = .5, wspace=.001)

figurecount = 1
for i in range(2,22,2):    
    model = AutoReg(dfUse, i)
    model_fit = model.fit()
    
    armodelString = 'AR order: ' + str(i)
    dftemp = pd.merge(pd.DataFrame(dfUse), pd.DataFrame(model_fit.fittedvalues), left_index=True, right_index=True)
    dftemp['RSS_elements'] = dftemp.apply(sum_residual_squares, axis=1) 
    residualList[i]=dftemp['RSS_elements'].sum()
    rss = "{:.2e}".format(dftemp['RSS_elements'].sum())
    print('lag = ' + str(i) + ' ,RSS: ' + rss )
    plt.subplot(2,5,figurecount)
    plt.plot(dfUse, label='_nolegend_', color="black", linewidth=2)
    plt.plot(model_fit.fittedvalues, label='_nolegend_', color="blue", linewidth=1)
    plt.title(armodelString)
    figurecount +=1

  ```

</details>


## 4. System (pip) and Modules

<details>
  <summary>Update package in google colab</summary>

  ```python

      !pip install statsmodels --upgrade

  ```

</details>
