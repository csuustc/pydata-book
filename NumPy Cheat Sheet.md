# NumPy Cheat Sheet

## NumPy Basics

```python
myarr = np.array(object, dtype= ) 
myarr.ndim
myarr.shape
myarr.dtype
myarr.astype(type) 
```

### Creating Arrays

```python
np.zeros() # create 0 array
np.ones()
np.full(size, value) # filled with value
np.linespace(start, end, n) # return an array n elements evenly spaced [start, end]
np.empty()
np.arange(start, stop, step)
np.eye(n) # creat n rank indentity matrix
np.random.randn(d0, d1, ...) # standard normal distribution
np.random.random(size) # uniform distribution [0, 1)
np.random.normal(mean, std, size) # normal distribution
np.random.randint(low, high, size) # discrete uniform
```



### Indexing and Slicing

```python
myarr[i, j] == myarr[i][j]
myarr[[0, 1, 2, 3]] # fancy indexing 
```

### Transposing

```python
myarr.T # transpose 2d array
np.dot(myarr.T, myarr) # dot product
myarr.transpose((1, 0, 2)) # 3d array transpose
myarr.swapaxes(0, 1) # same as above
```

### Universal Functions

```python
# ufuncs can set arguments out = arr 
np.sqrt(myarr) # square root
np.exp(myarr) # e expotential 
np.maximum(xarr, yarr)
reminder, whole_part = np.modf(myarr) # seperate interger and decimal
xarr, yarr = np.meshgrid(points, points) # output x y coordinates
```

## NumPy for Data Processing

```python
np.where(cond, xarr, yarr) # x if cond else y

```



