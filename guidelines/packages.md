# Pandex Development Guidelines - Packages
*2019-04-10*

## Data
`Pandas` will be the source data format for the plotting functions in the 
`pandex` package, as the name suggests. `Pandas` is convenient and widely used,
so I felt this was an obvious choice. Within the functions, however, it
is possible to use `numpy` data structures, since this may be more convenient or
required in some cases, e.g. in the base plotting functions or for math.

Compatibility with `dask`, as well as `dask.dataframe` and `dask.array`, is also a possibility, but is not being pursued at this time. The current plotting 
strategy requires the data to be contained within system memory for the
interactive plots to work, in which case the `dask` DataFrame could just be
converted to `pandas`. This unfortunately means that out-of-memory datasets cannot be analyzed with `pandex`, and will have to be reduced to a compatible size.

## Graphics
The graph/plot/visualization should appear in a separate window, with 
controls that can be used to select variables for each axis, and the plot
should update in real-time. Thus there are three frameworks being
considered.

### `Bokeh`
The `bokeh` package produces attractive visualizations and allows for real-time interactivity. This requires starting and running a `bokeh` server, but this can be handled locally, and started/stopped as needed when the plotting window is displayed. I have the most experience with `bokeh` which makes it a natural place to start.

### `Plotly`
I've had my eye on this package for some time. The visualizaitons look as good as `bokeh` but it doesn't seem to require Javascript, though React seems to be used under the hood. It will be worth exploring this option by writing equivalent but simple funcitons in both `bokeh` and `plotly`. Both seem to be equally aesthetically pleasing, so it will come down to which is more flexible.

### `Matplotlib` and `Tkinter`
There is a certain appeal to sticking with the "basic" plotting package, most coming from the possibly-reduced packacge dependencies. However `tkinter` would still be required to provide the interactivity. And this may end up turning into a case of reinvention of the wheel, since the desired functionality is readily available in both `bokeh` and `plotly`.
