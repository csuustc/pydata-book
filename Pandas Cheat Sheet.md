# Pandas Cheat Sheet

## Pandas Objects

### Series

```python
mySeries = pd.Series(data, index=[ ], dtype=, name= ) # can even use non-contiguous or non-sequential indices
mySeries.values # value's type is ndarray
mySeries.index # type index
mySeries.keys() # can use dictionary expression
mySeries.items()
mySeries.replace()
```

### DataFrame

```python
df = pd.DataFrame(data, index=[ ], columns=[ ])
df.index # same index as Series
df.columns # columns name, still Index
df.values
df.drop(labels=None, axis=0,
        index=None, columns=None,
        level=None, inplace=False) # drop rows or columns
```

### Index

```python
ind = pd.Index(data=, dtype=, name=) # like an immutable array
ind.name
ind.size 
ind.shape
ind.ndim
ind.dtype
ind.append() # append index element
ind.drop(labels) # drop index
ind.delete(loc) # delete ith index
ind.unique(level= )
```

### Categorical Data

```python
cat_s = df['str_col'].astype('category') # series of string to series of category
cat_s.cat.categories
cat_s.cat.codes
cat_s.cat.set_categories(new_categories, ordered=False)
```

## I/O

### Read and Loading

```python
pd.read_csv(filepath, sep=',', header, # int, list, None
            names, # list of column names
            index_col=None, # list of columns to use as index
            use_cols, # just use a subset of columns
            dtype, true_values, false_values, # set value as True of False
            skiprows, na_values, chunksize # read in piece
           )
# read in piece
chunker = pd.read_csv(filepath, chunksize=1000)
for piece in chunker:
    expr
```

### Writing

```python
df.to_csv(filepath, sep=',', header, index, ...)
```

### Interacting with Databases

```python
import sqlalchemy as sqla
db = sqla.create_engine('database path') # connect to database
pd.read_sql(sql, db) # use sql to query data
db.dispose() # shut down
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
df[conditions] # select rows under condition or whole boolean DataFrame
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

## Data Clean and Preparation

### Sorting

```python
df.sort_index(axis=0, level=None, # along axis
              ascending=True, inplace=False, kind='quicksort',
              na_position='last', sort_remaining=True, ignore_index: bool = False)
df.sort_values(by, # can be a list of str
               axis=0, ascending=True, inplace=False, 
               na_position='last', ignore_index=False)
df.rank(axis=0, method: str = 'average', # min, max, first
        numeric_only: Union[bool, NoneType] = None,
        na_option: str = 'keep', # or top, bottom
        ascending: bool = True,
        pct: bool = False # return percentage
       )
```

### Operating on Data

```python
pd.DataFrame.add(df1, df2, axis='columns', level=None, fill_value=None)
df1.add(df2, axis, level, fill_value)
```

| Python Operator | Pandas Method(s)                       |
| --------------- | -------------------------------------- |
| ``+``           | ``add()``                              |
| ``-``           | ``sub()``, ``subtract()``              |
| ``*``           | ``mul()``, ``multiply()``              |
| ``/``           | ``truediv()``, ``div()``, ``divide()`` |
| ``//``          | ``floordiv()``                         |
| ``%``           | ``mod()``                              |
| ``**``          | ``pow()``                              |


### Handling Missing Data

```python
df.isnull() # detect missing values
df.notnull() # opposite of isnull()
df.dropna(axis=0, how='any' or 'all', thresh= ) # set thresh as integer
df.fillna(value= , # can set dict to specify different values
          method= , axis= , limit= ) 
df.drop_duplicates(subset= , # list of columns
                   keep='first', 'last', None)
```

### Discretization and Binning

```python
cats = pd.cut(data, bins, # can be int or sequence
              right: bool = True, # whether includes right edge
              labels=None, # label for bins
             ) # return a categorical object
cats.codes
cats.categories
cats.value_counts()
cats = pd.qcut(data, q, # int or list, quantile
               labels=None, precision: int = 3)
```

### Outliers

```python
df[(np.abs(df) > 3 * np.std(df)).any(1)] # if 1 or more value > 3 sigma
df[(np.abs(df) > 3 * np.std(df)).any(1)] = np.sign(df) * 3 * np.std(df) 
```

### Random Sampling

```python
np.random.permutation(n) # Randomly permute a sequence
df.sample(n=None, frac=None, # get n samples or a fraction
          replace=False # get sample repeatly or not
          weights=None, random_state=None, axis=None)
```

### Dummy Variables

```python
dummies = pd.get_dummies(data, prefix=None, prefix_sep='_',
                         dummy_na=False, # Add a column to indicate NaNs
                         columns=None, drop_first=False, # make k-1 dummies
                         dtype=None)
df_with_dummy = df.drop('key').join(dummies)
```

## Hierarchical Indexing

### Multi Index Creation

```python
df = df.DataFrame(data, index=[[level1], [level2]]) # but cannot set index name
df = df.DataFrame(data, index=pd.Index([index], name=''),
                  columns=pd.MultiIndex.from_arrays(arrays, names=))
pd.MultiIndex(levels=None, codes=None, sortorder=None, names=None)
pd.MultiIndex.from_arrays(arrays, names= ) # Each array-like gives one level's value for each data point.
pd.MultiIndex.from_tuples(tuples, names= ) # Each tuple is the index of one row/column.
pd.MultiIndex.from_product(iterables, names = ) # cartesian product
df.index.names = [] # set index names
df.columns.names = [] # set columns names
```

### Rearranging index

```python
df.sort_index(axis=0, level=None, ascending=True, inplace=False) # sort index
df.stack(level=-1, dropna=True) # stack from columns to index
df.unstack(level=-1, fill_value=None) # unstack the inner-most level row
df.reindex(index=, columns =, # set new index
           method=, fill_value=, # set fill value
           level=, limit=)
df.reset_index(level=None, #remove all levels by default
               drop=False, name=None) # remove row labels to new columns
df.set_index(keys, drop=True, append=False) # set index using existing columns
df.rename(index=, columns=) # dict-like or func e.g. index=str.title
df.swaplevel(key1, key2, axis=0) # reorder levels
```

## Combining Datasets

### Concatenate and Append

```python
pd.concat(objs, axis=0, join='outer',
          ignore_index=False, # reset index
          keys=None, # specify a label for the data sources
          levels=None, names=None,
          verify_integrity=False) # verify_intergrity to check duplicate indices
df1.append(df2) # return a concated dataframe
```

### Merge and Join

```python
pd.merge(left, right, how: str = 'inner', 'outer', 'left', 'right',
         on=None, # label or list, must found in both df
         left_on=None, right_on=None, # if key's name different
         left_index: bool = False, right_index: bool = False, # use index as key
         sort: bool = False, # sort key
         suffixes=('_x', '_y'))
# join is a shortcut for merge, but can designate key, only on index
df1.join(df2, on=None, how='left', lsuffix='', rsuffix='', sort=False)
df.combine_first(other) # use other df to full NA value in df
```

## Aggregation and Transformation

| Aggregation              | Description                     |
| ------------------------ | ------------------------------- |
| ``count()``              | Total number of items           |
| ``first()``, ``last()``  | First and last item             |
| ``mean()``, ``median()`` | Mean and median                 |
| ``min()``, ``max()``     | Minimum and maximum             |
| ``idxmin()``, ``idxmax()``| return index of Minimum and maximum|
| ``std()``, ``var()``     | Standard deviation and variance |
| ``mad()``                | Mean absolute deviation         |
| ``prod()``               | Product of all items            |
| ``sum()``                | Sum of all items                |

### Mapping

```python
func = lambda x: x.max() - x.min()
df.apply(func, axis=0, ...) # for row or column
# e.g. count value for each column
df.apply(pd.value_counts).fillna(0)
df.applymap(func) # for each element
mySeries.map(func)
```

### Group by

```python
df.groupby(by=None, axis=1, level=None, as_index=True, sort=True)
# by can be a key, a list, a dic map, any python function
for name, group in df.groupby('key'):
    print(name, group)
pieces = dict(list(groupby('key')))
df.groupby('key')[columns].sum() 
df.groupby('key').aggregate([min, median, max]) # compute all the aggregates at once
df.groupby('key').aggregate({'data1': 'min', 'data2': 'max'})
df.groupby('key').filter(filter_func) # The filter function should return a Boolean value specifying whether the group passes the filtering
df.groupby('key').apply()
# transform return same shape with original dataframe
df.groupby('key').transform(lambda x: (x - x.mean()) / x.std()) 
```

### Pivot Table

```python
df.pivot_table(values=None, # column to aggregate
               index=None, columns=None, 
               aggfunc='mean', fill_value=None, # can apply multi funcs
               margins=False, margins_name='All', # total row / columns
               dropna=True)
# df.pivot is more simple, but cannot aggregate
df.pivot(index=None, columns=None, values=None) # from 'long' data to pivot
# crosstab similar to pivot_table, but use when don't have dataframe
pd.crosstab(index, columns, values=None, # all array-like
            rownames=None, colnames=None,
            aggfunc=None, margins=False)
# from wide to long, use melt or stack
df.melt(id_vars=None, # the key column, which won't change
        value_vars=None, # columns gonna stack
        var_name=None, # new stacked column
        value_name='value', col_level=None)
# difference is that stack return stacked column as index, melt as a new column
```

## String Operations

### Str. Methods

```python
mySeries.str.upper()
```

|              |                  |                  |                  |
| ------------ | ---------------- | ---------------- | ---------------- |
| ``len()``    | ``lower()``      | ``translate()``  | ``islower()``    |
| ``ljust()``  | ``upper()``      | ``startswith()`` | ``isupper()``    |
| ``rjust()``  | ``find()``       | ``endswith()``   | ``isnumeric()``  |
| ``center()`` | ``rfind()``      | ``isalnum()``    | ``isdecimal()``  |
| ``zfill()``  | ``index()``      | ``isalpha()``    | ``split()``      |
| ``strip()``  | ``rindex()``     | ``isdigit()``    | ``rsplit()``     |
| ``rstrip()`` | ``capitalize()`` | ``isspace()``    | ``partition()``  |
| ``lstrip()`` | ``swapcase()``   | ``istitle()``    | ``rpartition()`` |

### Regular Expressions

| Method         | Description                                                  |
| -------------- | ------------------------------------------------------------ |
| ``match()``    | Call ``re.match()`` on each element, returning a boolean.    |
| ``extract()``  | Call ``re.match()`` on each element, returning matched groups as strings. |
| ``findall()``  | Call ``re.findall()`` on each element                        |
| ``replace()``  | Replace occurrences of pattern with some other string        |
| ``contains()`` | Call ``re.search()`` on each element, returning a boolean    |
| ``count()``    | Count occurrences of pattern                                 |
| ``split()``    | Equivalent to ``str.split()``, but accepts regexps, e.g. '\s+' for space |
| ``rsplit()``   | Equivalent to ``str.rsplit()``, but accepts regexps          |
| ``get()`` | Index each element |
| ``slice()`` | Slice each element|
| ``slice_replace()`` | Replace slice in each element with passed value|
| ``cat()``      | Concatenate strings|
| ``repeat()`` | Repeat values |
| ``normalize()`` | Return Unicode form of string |
| ``pad()`` | Add whitespace to left, right, or both sides of strings|
| ``wrap()`` | Split long strings into lines with length less than a given width|
| ``join()`` | Join strings in each element of the Series with passed separator|
| ``get_dummies()`` | extract dummy variables as a dataframe |

## Time Series

## Eval and Query

```python
pd.eval(expr) # uses string expressions to efficiently compute operations
df.eval(expr) # treat column names as variables within the evaluated expression, but can't filter
df.query(expr) # Query the columns of a DataFrame with a boolean expression
```



