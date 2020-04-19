# Pandas Cheat Sheet

## Pandas Objects

### Series

```python
mySeries = pd.Series(data, index=[ ]) # can even use non-contiguous or non-sequential indices
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
df.at[label_i, label_j] # select one value using label
df.iat[i, j] # use integer index

```

