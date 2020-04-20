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



