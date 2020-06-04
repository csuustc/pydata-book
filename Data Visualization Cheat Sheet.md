# Data Visualization Cheat Sheet

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
fig, ax = plt.subplots(nrows=1, ncols=1, sharex=False, sharey=False)
# Call plot() method on the appropriate object
ax[ ].plot()

fig.savefig('my_figure.png') # save picture
```

### Subplots

```python
# Subplots by Hand
fig = plt.figure(num=None, figsize=None, dpi=None, facecolor=None, edgecolor=None)
ax = plt.axes([left, bottom, width, height])
ax_i = fig.add_axes( )
ax_i = fig.add_subplot(nrows, ncols, i)
# simple grids
plt.subplot(nrows, ncols, index, **kwargs)
# multi grids
fig, ax = plt.subplots(nrows, ncols, sharex=False, sharey=False)
# adjust the spacing between these plots
plt.subplots_adjust(left, bottom, right, top, wspace, hspace)
```

## Plots

### Line Plots

```python
plt.plot([x], y, [fmt], *, data= , **kwargs)
# kwargs
color or c 
linestyle or ls = '-' 'solid', '--' 'dashed', '-.' 'dashdot', ':' 'dotted'
linewidth or lw = 
label = 
marker = '.' point marker, ',' pixel marker, 'o' circle marker, 's' square marker ...
# format strings (fmt)
fmt = '[marker][line][color]' or '[color][marker][line]' # e.g. 'o--g' 'r-.'
```

### Scatter Plots

```python
plt.plot(x, y, marker=) # Scatter can be individually controlled or mapped to data.
plt.scatter(x, y, s=None,# size can be array to map data
            c=None, # color can be sequance of color or sequance of number then cmap
            marker=None,
            cmap=None, # *cmap* is only used if *c* is an array of floats.
            alpha=None, # transparent value
            linewidths=None, # linewidth of the marker edges
            edgecolors=None
           )
plt.colorbar()  # show color scale
plt.cm.<TAB> # browse color map
# plt.plot should be preferred over plt.scatter for large datasets
```

### Error Bars

```python
plt.errorbar(x, y, yerr=None, xerr=None, fmt='', ecolor=None, 
             elinewidth=None, capsize=None) # discrete value
plt.fill_between(xfit, yfit - dyfit, yfit + dyfit) # continuous value
```

### Histograms

```python
plt.hist(x, bins=None, # if a number, then divide bins; if sequence, then edges 
         range=None, density=None, # if true, first element's area will be 1
         weights=None, cumulative=False, bottom=None, histtype='bar',
         align='mid', orientation='vertical', rwidth=None, color=None,
         label=None, stacked=False)
plt.hist2d(x, y, bins=10, range=None, density=False, cmap='')
```

### 3-D plotting

```python
from mpl_toolkits import mplot3d
ax = plt.axes(projection='3d')
ax.plot3D(x, y, z) # plot a line
ax.scatter3D(xdata, ydata, zdata) # scatters
ax.view_init() # rotate viewing angles
# Wireframes and surface
ax.plot_wireframe(X, Y, Z)
ax.plot_surface(X, Y, Z)
```

## Customizing

### Legends

```python
plt.legend((line1, line2), ('label1', 'label2'), loc='best' '0', 'upper right' '1'...
           frameon='True', ncol= )
```

### Colorbars

```python
plt.imshow(X, cmap=plt.cm.get_cmap('Blues', 6), ticks= ) # here for concrete color
plt.colorbar()
plt.clim(vmin= , vmax= ) # set colorbar limit
```

### Text and Annotation

```python
plt.text(x, y, s, fontdict=None, ha='center', va='center', **kwargs) # Add the text *s*
# text position
ax.text(x, y, s, transform=ax.transData # data coordinate
        transform=ax.transAxes # axes
        transform=fig.transFigure) # figure
# arrow and annotation
plt.annotate(s, xy, # point to annotate
             xytext, # position to place text
             arrowprops=dict(arrowstyle, width, shrink, ...))
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

### Axis

```python
plt.xlim(xleft, xright) # ax.set_xlim
plt.ylim(yleft, yright)
plt.axis([xmin, xmax, ymin, ymax])
plt.axis('tight', 'equal'...)
ax.set_xticks(ticks) # list of ticks location
ax.set_xticklabels(labels) # set label for ticks
ax.xaxis.set_major_locator(plt.NullLocator())
```

| Locator class        | Description                                             |
| -------------------- | ------------------------------------------------------- |
| ``NullLocator``      | No ticks                                                |
| ``FixedLocator``     | Tick locations are fixed                                |
| ``IndexLocator``     | Locator for index plots (e.g., where x = range(len(y))) |
| ``LinearLocator``    | Evenly spaced ticks from min to max                     |
| ``LogLocator``       | Logarithmically ticks from min to max                   |
| ``MultipleLocator``  | Ticks and range are a multiple of base                  |
| ``MaxNLocator``      | Finds up to a max number of ticks at nice locations     |
| ``AutoLocator``      | (Default.) MaxNLocator with simple defaults.            |
| ``AutoMinorLocator`` | Locator for minor ticks                                 |

| Formatter Class        | Description                             |
| ---------------------- | --------------------------------------- |
| ``NullFormatter``      | No labels on the ticks                  |
| ``IndexFormatter``     | Set the strings from a list of labels   |
| ``FixedFormatter``     | Set the strings manually for the labels |
| ``FuncFormatter``      | User-defined function sets the labels   |
| ``FormatStrFormatter`` | Use a format string for each value      |
| ``ScalarFormatter``    | (Default.) Formatter for scalar values  |
| ``LogFormatter``       | Default formatter for log axes          |

### Stylesheets

```python
plt.rc('axes', facecolor= , edgecolor= , grid=True, prop_cycle=colors)
plt.rc('grid', color= , linestyle='solid')
plt.rc('xtick', direction='out', color= )
plt.rc('ytick', direction='out', color= )
plt.rc('figure', figsize=(10, 10))
plt.rc('patch', edgecolor= )
plt.rc('lines', linewidth= )
plt.style.available # to see styles
plt.style.use()
```

## Seaborn

```python
import seaborn as sns
sns.set() # set style as seaborn
sns.regplot(x, y, data)
sns.kdeplot(data) # smooth estimate of the distribution using a kernel density estimation
sns.distplot(data) # hist and KDE
sns.jointplot(x, y, data, kind= ) # 'reg', ...
sns.pairplot(data, hue=None, # categorical variable
             hue_order=None, palette=None, # color palette to use
             vars=None, x_vars=None, y_vars=None, # variables to use
             kind='scatter', or 'reg'
             diag_kind='auto', 'hist', 'kde', None)
# Faceted histograms
grid = sns.FacetGrid(data, row=None, col=None, hue=None...)
grid.map(plotfunc, data, ...) # apply a plot to each facet's data
# for categorical data
sns.catplot(x, y, hue, data, row, col, kind, color)
sns.violinplot()
```







