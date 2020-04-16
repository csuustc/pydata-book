# Python Basics Cheat Sheet

## Python Language Basics

```python
a // b # integer division
a ** b # power
a % b # residual
a is b # 'is' check if same object, maybe a == b, but a is not b 
isinstance(x, int) # check if object in the class
```

### Strings

```python
mystr.count('')
mystr.replace('old', 'new') # return a new string
'{0:.2f} {1:s} {2:d}'.format( , , ) # '.2f' float, 's' string, 'd' int
mystr.encode('utf-8') # encode from bytes to utf-8
mystr.decode('utf-8') # decode from utf-8 to bytes
```

### Date and Time

```python
from datetime import datetime, date, time
dt = datetime(2011, 10, 29, 20, 30, 21)
dt.day
dt.minute
dt.date()
dt.time()
dt.strftime('%m/%d/%Y %H:%M') # datetime to string
datetime.strptime() # string to datetime
```

### Loop

```python
for i in sequence:
    if:
        continue # go out this loop, go on next loop value
    elif:
        pass # do nothing
    else:
        break # stop loop
```

### Magic Commands

```python
%run # run external code
%pwd # print working directory
%ls # list working directory contents
%cd # change directory
%time # 1 time execution
%timeit # repeated execution
%prun # profiling full scripts
%lprun # line-by-line profiling
%memit # memory measuring
%mprun # line-by-line memory profiler
```

## Data Structures and Sequences

### Tuple

```python
# immutable, but element mutable
a, b, (c, d) = 1, 2, (3, 4) # unpacking
a, b, *_ = (1, 2, 3, 4)
seq = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]
for a, b, c in seq: # for iteration
    expr
```

### List

```python
mylist.append() # append object as single element at last
mylist.extend() # add each element to the list
mylist.insert(index= , object= ) # need more computation
mylist.pop(index=-1) # reverse to insert
mylist.sort(key= ) # sort inplace
sorted(mylist, key= ) # sorted can use in any iterable and return a  new list
mylist[i:j] # slicing
mylist[::n] # jump n
zip(mylist1, mylist2) # zip packing
for i, (a, b) in enumerate(zip(mylist1, mylist2)): 
    expr
mylist1, mylist2 = zip(*mylist) # * to unpack
[expr for val in collection if condition] # list comprehensions (same as dict, set)
```

### Dictionary

```python
mydict.keys() # list of keys
mydict.values() # list of values
mydict.pop(key) # drop key item and return value
mydict.update({'key': value})
mydict.get(key, default_value) # return dict[key] if exist, otherwise default
mydict.setdefault(key, default_value) # get mydict[key], else set mydict[key] as default
hash() # check hashable, key must be immutable
```

### Set

```python
# mutable, but element immutable
set_a.union(set_b) # same as set_a | set_b
set_a.intersection(set_b) #same as set_a & set_b
set_a.add() # add another element
set_a.remove() # delete an element
set_a.issubset(set_b)
set_a.issuperset(set_b)
```

## Functions 

### Generator

```python
def gen(n): # return 1 value until next call
    for i in range(n):
        yield i ** 2
gen = (x ** 2 for x in range(n)) # generator comprehension
```

### Errors and Exception

```python
try:
    # e.g. open(path)
except: # TypeError, ValueError
    # return 'Error'
else:
    # if try succeeded, then operate else
finally:
    #no matter try succeed or fail
```

## Files and Operating System

```python
with open(path) as f: # with can close file after use
    lines = [x.strip() fro x in f]
f.writelines()
f.readlines()
f.read(n) # read n characters
f.tell() # return present address
```

