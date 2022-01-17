# Python_CheatSheet
Python_CheatSheet

## 1. - [Python_CheatSheet](#python_cheatsheet)
  - [1. Dataframe Operations](#1-dataframe-operations)
  - 

## Dataframe Operations

1. Dataframe summary
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