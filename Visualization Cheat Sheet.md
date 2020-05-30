# Visualization Cheat Sheet

## Basics

```python
plt.style.use('classic') # seaborn-whitegrid
%matplotlib inline

# MATLAB-style
plt.figure()  # create a plot figure
# create the first of two panels and set current axis
plt.subplot(2, 1, 1) # (rows, columns, panel number)
plt.plot(x, np.sin(x))
# create the second panel and set current axis
plt.subplot(2, 1, 2)
plt.plot(x, np.cos(x))

# Object-oriented interface
# First create a grid of plots
# ax will be an array of two Axes objects
fig, ax = plt.subplots(nrows=1, ncols=1, sharex=False, sharey=False)
# Call plot() method on the appropriate object
ax[ ].plot()

# if only 1 figure
fig = plt.figure(num=None, figsize=None, dpi=None, facecolor=None, edgecolor=None)
ax = plt.axes()

fig.savefig('my_figure.png') # save picture
```

## Line Plots

```python
plt.plot([x], y, [fmt], *, data= , **kwargs)
# kwargs
color or c 
linestyle or ls = '-' 'solid', '--' 'dashed', '-.' 'dashdot', ':' 'dotted'
linewidth or lw = 
label = 
marker = '.' point marker, ',' pixel marker, 'o' circle marker, 's' square marker ...
# format strings (fmt)
fmt = '[marker][line][color]' # e.g. 'o--g' '-.r'
```

### Adjusting plots

```python
plt.xlim(xleft, xright) # ax.set_xlim
plt.ylim(yleft, yright)
plt.axis([xmin, xmax, ymin, ymax])
plt.axis('tight', 'equal'...)
```

### Labeling

```python
plt.title(label, fontdict=None, loc='center', pad=None, **kwargs) # ax.set_title
plt.xlabel(xlabel, fontdict=None, labelpad=None, **kwargs) # ax.set_xlabel
plt.ylabel() # ax.set_ylabel
plt.legend()
# more convenient way
ax.set(xlim= , ylim= , xlabel='', ylabel='', title='');
```

