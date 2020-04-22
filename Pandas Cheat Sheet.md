# Pandas Cheat Sheet

## Pandas Objects

### Series

```python
mySeries = pd.Series(data, index=[ ], dtype=, name= ) # can even use non-contiguous or non-sequential indices
mySeries.values # value's type is ndarray
mySeries.index # type index
mySeries.keys() # can use dictionary expression
mySeries.items()
```

### DataFrame

```python
df = pd.DataFrame(data, index=[ ], columns=[ ])
df.index # same index as Series
df.columns # columns name, still Index
df.values
```

### Index

```python
ind = pd.Index() # like an immutable array
ind.size 
ind.shape
ind.ndim
ind.dtype
```

## Indexing and Selection

### Slicing in Series

```python
mySeries['one': 'three'] # include end
mySeries.loc() # use explicit index
mySeries.iloc # use implicit Python-style index
```

### Slicing in DataFrame

```python
df[columns] # select one or more columns, also df.column
df[conditions] # select rows under condition
df[ : ] # select rows
df.loc[indexes] # select one or more rows
df.loc[:, columns] # select one or more columns
df.loc[ , ] # row & columns
df.iloc[where] # rows
df.iloc[:, where] # columns
df.ix[ , ] # can combine explicit and implicit index
df.at[label_i, label_j] # select one value using label
df.iat[i, j] # use integer index
```

## Operating on Data

| Python Operator | Pandas Method(s)                       |
| --------------- | -------------------------------------- |
| ``+``           | ``add()``                              |
| ``-``           | ``sub()``, ``subtract()``              |
| ``*``           | ``mul()``, ``multiply()``              |
| ``/``           | ``truediv()``, ``div()``, ``divide()`` |
| ``//``          | ``floordiv()``                         |
| ``%``           | ``mod()``                              |
| ``**``          | ``pow()``                              |

## Handling Missing Data

```python
df.isnull() # detect missing values
df.notnull() # opposite of isnull()
df.dropna(axis=0, how='any' or 'all', thresh= ) # set thresh as integer
df.fillna(value= , method= , axis= , limit= ) 
```

## Hierarchical Indexing

### Multi Index Creation

```python
df = df.DataFrame(data, index=[[level1], [level2]]) # but cannot set index name
pd.MultiIndex(levels=None, codes=None, sortorder=None, names=None)
pd.MultiIndex.from_arrays(arrays, names= ) # Each array-like gives one level's value for each data point.
pd.MultiIndex.from_tuples(tuples, names= ) # Each tuple is the index of one row/column.
pd.MultiIndex.from_product(iterables, names = ) # cartesian product
df.index.names = [] # set index names
df.columns.names = [] # set columns names
```

### Rearranging Multi-Indices

```python
df.sort_index(axis=0, level=None, ascending=True, inplace=False) # sort index
df.stack(level=-1, dropna=True) # stack from columns to index
df.unstack(level=-1, fill_value=None) # unstack the inner-most level row
df.reindex() # change index as 
df.reset_index(level=None(remove all levels by default), drop=False, name=None(value name)) # remove row labels to new columns
df.set_index(keys, drop=True, append=False) # set index using existing columns
```

## Combining Datasets

### Concatenate and Append

```python
pd.concat(objs, axis=0, join='outer', join_axes=None, ignore_index=False,
          keys=None, levels=None, names=None, verify_integrity=False)
# verify_intergrity to check duplicate indices
# keys to specify a label for the data sources
# join_axes to specify the columns after join
df1.append(df2) # return a concated dataframe
```

### Merge and Join

```python
pd.merge(left, right,
    how: str = 'inner', 'outer', 'left', 'right'
    on=None, # label or list, must found in both df
    left_on=None, right_on=None, # if key's name different
    left_index: bool = False, right_index: bool = False, # use index as key
    sort: bool = False, # sort key
    suffixes=('_x', '_y'))
df1.join(df2, on=None, how='left', lsuffix='', rsuffix='', sort=False)
```

## Aggregation

| Aggregation              | Description                     |
| ------------------------ | ------------------------------- |
| ``count()``              | Total number of items           |
| ``first()``, ``last()``  | First and last item             |
| ``mean()``, ``median()`` | Mean and median                 |
| ``min()``, ``max()``     | Minimum and maximum             |
| ``std()``, ``var()``     | Standard deviation and variance |
| ``mad()``                | Mean absolute deviation         |
| ``prod()``               | Product of all items            |
| ``sum()``                | Sum of all items                |

### Group by

```python
df.groupby(by=None, axis=1, level=None, as_index=True, sort=True)
# by can be a key, a list, a dic map, any python function
df.groupby('key')[volumns].sum() 
df.groupby('key').aggregate([min, median, max]) # compute all the aggregates at once
df.groupby('key').aggregate({'data1': 'min', 'data2': 'max'})
df.groupby('key').filter(filter_func) # The filter function should return a Boolean value specifying whether the group passes the filtering
df.groupby('key').transform(lambda x: x - x.mean()) # return some transformed version of the full data to recombine
df.groupby('key').apply()
```

### Pivot Table

```python
df.pivot_table(values=None, # column to aggregate
    index=None, columns=None, aggfunc='mean', fill_value=None, # can apply multi funcs
    margins=False, margins_name='All', # total row / columns
    dropna=True)
```