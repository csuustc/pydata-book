# NumPy Cheat Sheet

## NumPy Basics

### NumPy Array Attributes

```python
myarr.ndim # dimensions
myarr.shape
myarr.size # total size
myarr.dtype # myarr.astype(type) 
myarr.itemsize # byte size of each element
myarr.nbytes # total byte size
```

### Creating Arrays

```python
np.zeros(shape, dtype=float, order='C') # create 0 array
np.ones() # np.ones_like
np.full(size, value) # filled with value
np.linspace(start, end, n) # return an array n elements evenly spaced [start, end]
np.empty() # np.empty_like
np.arange(start, stop, step)
np.eye(n) # creat n rank indentity matrix
np.repeat(arr, repeats, axis) # repeats can be a single number or a list
np.tile(arr, reps) # duplicate while array
```
### Indexing and Slicing

```python
myarr[start : stop : step] # if step negative, then swap start and stop
myarr[i, j] == myarr[i][j]
myarr[myarr < 0] = 0 # index by boolean array
myarr[[0, 1, 2, 3]] # fancy indexing 
myarr.take(indices, axis) # similiar to fancy indexing
myarr.put(indices, value) # value can be a list
```

![Figure 4-2. Two-dimensional array slicing](/Users/changsu/Google Drive/coursework/pydata-book/picture/Figure 4-2. Two-dimensional array slicing.png)

### Pseudorandom

```python
np.random.seed() # global seed
np.random.RandomState(seed).randn() # local seed
np.random.randn(d0, d1, ...) # standard normal distribution
np.random.random(size) # uniform distribution [0, 1)
np.random.normal(mean, std, size) # normal distribution
np.random.randint(low, high, size) # discrete uniform
np.random.permutation() # random permutation
np.random.shuffle() # Modify a sequence in-place
np.random.gamma() # binomial, beta, chisquare....
```

### Data Type

| Character        | Description            | Example                              |
| ---------------- | ---------------------- | ------------------------------------ |
| ``'b'``          | Byte                   | ``np.dtype('b')``                    |
| ``'i'``          | Signed integer         | ``np.dtype('i4') == np.int32``       |
| ``'u'``          | Unsigned integer       | ``np.dtype('u1') == np.uint8``       |
| ``'f'``          | Floating point         | ``np.dtype('f8') == np.float64``     |
| ``'c'``          | Complex floating point | ``np.dtype('c16') == np.complex128`` |
| ``'S'``, ``'a'`` | String                 | ``np.dtype('S5') == np.string_``     |
| ``'U'``          | Unicode string         | ``np.dtype('U') == np.str_``         |
| ``'V'``          | Raw data (void)        | ``np.dtype('V') == np.void``         |

```python
# NumPy dtype Hierarchy
np.issubdtype(np.float64, np.float)
np.issubdtype(np.int16, np.integer)
# nested dtype like pd dataframe
dtype = [('x', [('a', 'f8'), ('b', 'f4')]), ('y', np.int32)]
```

## Universal Functions

### Arithmetic Operators

| Operator | Equivalent ufunc    | Description                              |
| -------- | ------------------- | ---------------------------------------- |
| ``+``    | ``np.add``          | Addition (e. g., ``1 + 1 = 2``)          |
| ``-``    | ``np.subtract``     | Subtraction (e. g., ``3 - 2 = 1``)       |
| ``-``    | ``np.negative``     | Unary negation (e. g., ``-2``)           |
| ``*``    | ``np.multiply``     | Multiplication (e. g., ``2 * 3 = 6``)    |
| ``/``    | ``np.divide``       | Division (e. g., ``3 / 2 = 1.5``)        |
| ``//``   | ``np.floor_divide`` | Floor division (e. g., ``3 // 2 = 1``)   |
| ``**``   | ``np.power``        | Exponentiation (e. g., ``2 ** 3 = 8``)   |
| ``%``    | ``np.mod``          | Modulus/remainder (e. g., ``9 % 4 = 1``) |

```python
# ufuncs can set arguments out = arr 
np.sqrt(myarr) # square root
np.exp(myarr) # e expotential 
np.exp2(myarr) # 2^x
np.power(n, myarr) # n^x
np.cumsum # cumulated sum
np.cumprod # cumulated product
np.log(myarr) # ln()
np.log2(myarr) # log2()
np.log10(myarr) # log10()
np.maximum(xarr, yarr)
np.multiply.outer(xarr, yarr) # outer product
np.dot(xarr, yarr) # dot product
xarr @ yarr # dot product
xarr * yarr # element-wise product
reminder, whole_part = np.modf(myarr) # seperate interger and decimal
np.allclose(xarr, yarr) # Returns True if two arrays are element-wise equal within a tolerance
```

### Aggregation Operations

| Function Name     | NaN-safe Version     | Description                               |
| ----------------- | -------------------- | ----------------------------------------- |
| ``np.sum``        | ``np.nansum``        | Compute sum of elements                   |
| ``np.prod``       | ``np.nanprod``       | Compute product of elements               |
| ``np.mean``       | ``np.nanmean``       | Compute mean of elements                  |
| ``np.std``        | ``np.nanstd``        | Compute standard deviation                |
| ``np.var``        | ``np.nanvar``        | Compute variance                          |
| ``np.min``        | ``np.nanmin``        | Find minimum value                        |
| ``np.max``        | ``np.nanmax``        | Find maximum value                        |
| ``np.argmin``     | ``np.nanargmin``     | Find index of minimum value               |
| ``np.argmax``     | ``np.nanargmax``     | Find index of maximum value               |
| ``np.median``     | ``np.nanmedian``     | Compute median of elements                |
| ``np.percentile`` | ``np.nanpercentile`` | Compute rank-based statistics of elements |
| ``np.any``        | N/A                  | Evaluate whether any elements are true    |
| ``np.all``        | N/A                  | Evaluate whether all elements are true    |

### Other Logic Operation

```python
# return same shape as condition array
np.where(cond, xarr, yarr) # if cond = True, x; else y
np.unique(myarr, return_index=False, return_counts=False, axis=None)
np.in1d(xarr, yarr) # whether each element of x is contained in y
xarr, yarr = np.meshgrid(points, points) # output x y coordinates
```

## Transformation

### Reshaping and Transposing

```python
myarr.reshape((i, j)) # return a new array, fill -1 can auto fill
myarr.ravel() # retrun a flattern view
myarr.flatten() # return a flatter copy
myarr.T # transpose 2d array
np.dot(myarr.T, myarr) # dot product
myarr.transpose((1, 0, 2)) # 3d array transpose
myarr.swapaxes(0, 1) # same as above
# arr.T is accutally arr.swapaxes(0, -1)
myarr[:, np.newaxis] # reshape
```

### Sorting

```python
np.sort(myarr, axis=-1) # return a sorted array
myarr.sort(axis=-1) # sort in place
myarr[:, ::-1] # reverse sort
myarr.searchsorted(value) # assume myarr is sorted
np.argsort(myarr, axis=-1) # return sorted index
np.partition(myarr, kth, axis) # smallest K values
np.argpartition() # index
```

### Concatenation and Splitting

```python
np.concatenate([arrays], axis=0) 
np.vstack() # vertical stack (axis = 0)
np.hstack() # horizontal stack (axis = 1)
# stacking helpers
np.r_[arr1, arr2] # same as vstack
np.c_[arr1, arr2] # same as hstack
np.split(myarr, indices_or_sections, axis=0) # split into N sections or a list of indices
np.vsplit() # vertical split
np.hsplit() # horizontal split
```

## Broadcasting

**The Broadcasting Rule**: Two arrays are compatible for broadcasting if for each trailing dimension (i.e., starting from the end) the axis lengths match or if either of the lengths is 1. Broadcasting is then performed over the missing or length 1 dimensions.

```python
arr2d - arr2d.mean(0) # arr2d.shape = (i, j), arr2d.mean(0).shape = (j,)
arr2d - arr2d.mean(1).reshape(j, 1) 
# setting values
arr2d.shape = (i, j), col[:, np.newaxis].shape = (j, 1)
arr[:] = col[:, np.newaxis] # fill arr use col
```







