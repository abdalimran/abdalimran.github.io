---
layout: post
title: Faster Pandas Operation with Swifter
category: 
    - "Miscellaneous"
---

As data professionals, we use Pandas most of the time for a variety of data processing tasks. 
When it comes to applying user-defined functions (UDFs) on a pandas series (or column), we face performance issues for large datasets.
An awesome solution to this performance issue is to use **Swifter**. 
The swifter algorithm has enabled performant pandas applies for user-defined functions (UDFs). 
The algorithm leverages a combination of attempting to execute the quick solution (vectorization), 
estimation and extrapolation, and validation of output to ensure that dataframe applies are swift and accurate.
Due to swifter’s algorithmic approach, dataframe applies automatically converge to 
either serial or multiprocessing dependent on the size of the data and complexity of the function applied.

The impact made by the swifter algorithm is best captured by the following [performance benchmark](https://github.com/jmcarpenter2/swifter/blob/master/examples/swifter_speed_comparison.ipynb).

Now, let’s try to see Swifter in action.

## Installation:
```
$ pip install -U pandas # upgrade pandas
$ pip install swifter # first time installation

$ pip install -U swifter # upgrade to latest version if already installed
```

alternatively, to install on [Anaconda](https://anaconda.org/conda-forge/swifter):
```
conda install -c conda-forge swifter
```

...after installing, import `swifter` into your code along with `pandas` using:
```python
import pandas as pd
import swifter
```

...alternatively, `swifter` can be used with `modin` dataframes in the same manner:
```python
import modin.pandas as pd
import swifter
```
**NOTE:** 
1. If you import swifter before modin, you will have to additionally register modin: `swifter.register_modin()`
2. Please upgrade your version of pandas, as the pandas extension api used in this module is a recent addition to pandas.
3. Do not use swifter to apply a function that modifies external variables. Under the hood, swifter does sample applies to optimize performance. These sample applies will modify the external variable in addition to the final apply. Thus, you will end up with an erroneously modified external variable.
4. It is advised to disable the progress bar if calling swifter from a forked process as the progress bar may get confused between various multiprocessing modules.

## 1. `pandas.Series.swifter.apply` OR `modin.pandas.Series.swifter.apply`

Efficiently apply any function to a pandas series in the fastest available manner

```python
def pandas.Series.swifter.apply(func, convert_dtype=True, args=(), **kwds)
```

**Parameters:**

`func` : function. Function to apply to each element of the series.

`convert_dtype` : boolean, default True. Try to find better dtype for elementwise function results. If False, leave as dtype=object

`args` : tuple. Positional arguments to pass to function in addition to the value

`kwds` : Additional keyword arguments will be passed as keywords to the function

NOTE: docstring taken from pandas documentation.


## 2. `pandas.DataFrame.swifter.apply` OR `modin.pandas.DataFrame.swifter.apply`

Efficiently apply any function to a pandas dataframe in the fastest available manner.

```python
def pandas.DataFrame.swifter.apply(
        func, 
        axis=0, 
        raw=False, 
        result_type=None,
        args=(), 
        **kwds
    )
```

**Parameters:**

`func` : function. Function to apply to each column or row.

`axis` : {0 or 'index', 1 or 'columns'}, default 0. **For now, Dask only supports axis=1, and thus swifter is limited to axis=1 on large datasets when the function cannot be vectorized.** Axis along which the function is applied:

* 0 or 'index': apply function to each column.
* 1 or 'columns': apply function to each row.

`raw` : bool, default False
False : passes each row or column as a Series to the function.
True : the passed function will receive ndarray objects instead. If you are just applying a NumPy reduction function this will achieve much better performance.

`result_type` : {'expand', 'reduce', 'broadcast', None}, default None. These only act when axis=1 (columns):

'expand' : list-like results will be turned into columns.
'reduce' : returns a Series if possible rather than expanding list-like results. This is the opposite of 'expand'.
'broadcast' : results will be broadcast to the original shape of the DataFrame, the original index and columns will be retained.
The default behaviour (None) depends on the return value of the applied function: list-like results will be returned as a Series of those. However if the apply function returns a Series these are expanded to columns.

`args` : tuple. Positional arguments to pass to func in addition to the array/series.

`kwds` : Additional keyword arguments to pass as keywords arguments to func.

NOTE: docstring taken from pandas documentation.

**returns:**

The new dataframe/series with the function applied as quickly as possible

## 3. `pandas.DataFrame.swifter.applymap`

Efficiently applymap any function to a pandas dataframe in the fastest available manner. Applymap is elementwise.

```python
def pandas.DataFrame.swifter.applymap(func)
```

## 4. `pandas.DataFrame.swifter.rolling.apply`

Applies over a rolling object on the original series/dataframe in the fastest available manner.

```python
def pandas.DataFrame.swifter.rolling(
        window, 
        min_periods=None, 
        center=False, 
        win_type=None, 
        on=None, 
        axis=0, 
        closed=None
    ).apply(func, *args, **kwds)
```

## 5. `pandas.DataFrame.swifter.resample.apply`

Applies over a resampler object on the original series/dataframe in the fastest available manner.

```python
def pandas.DataFrame.swifter.resample(
        rule,
        axis=0,
        closed=None,
        label=None,
        convention="start",
        kind=None,
        loffset=None,
        base=0,
        on=None,
        level=None,
        origin=None,
        offset=None,
    ).apply(func, *args, **kwds)
```

## 6. `pandas.DataFrame.swifter.progress_bar(False).apply`

Enable or disable the TQDM progress bar by setting the enable parameter to True/False, respectively. You can also specify a custom description.

Note: It is advised to disable the progress bar if calling swifter from a forked process as the progress bar may get confused between various multiprocessing modules. 

```python
def pandas.DataFrame.swifter.progress_bar(enable=True, desc=None)
```

For example, let's say we have a pandas dataframe df. The following will perform a swifter apply, without the TQDM progress bar.

```python
df.swifter.progress_bar(False).apply(lambda x: x+1)
```

## 7. `pandas.DataFrame.swifter.set_npartitions(npartitions=None).apply`

Specify the number of partitions to allocate to swifter, if parallel processing is chosen to be the quickest apply.
If npartitions=None, it defaults to cpu_count()*2

```python
def pandas.DataFrame.swifter.set_npartitions(npartitions=None)
```

For example, let's say we have a pandas dataframe df. The following will perform a swifter apply, using 2 partitions
```python
df.swifter.set_npartitions(2).apply(lambda x: x+1)
```

## 8. `pandas.DataFrame.swifter.set_ray_compute(num_cpus=None, memory=None, **kwds).apply`

Set the amount of compute used by ray for modin dataframes.

`num_cpus`: the number of cpus used by ray multiprocessing

`memory`: the amount of memory allocated to ray workers

If a proportion of 1 is provided (0 < memory <= 1],
    then that proportion of available memory is used

If a value greater than 1 is provided (1 < memory <= virtual_memory().available]
    then that many bytes of memory are used

`kwds`: key-word arguments to pass to `ray.init()`

```python
def pandas.DataFrame.swifter.set_ray_compute(num_cpus=None, memory=None, **kwds)
```

For example, let's say we have a pandas dataframe df. The following will perform a swifter apply, using 2 partitions
```python
df.swifter.set_npartitions(2).apply(lambda x: x+1)
```

## 9. `pandas.DataFrame.swifter.set_dask_threshold(dask_threshold=1).apply`

Specify the dask threshold (in seconds) for the max allowable time estimate for a pandas apply on the full dataframe
```python
def pandas.DataFrame.swifter.set_dask_threshold(dask_threshold=1)
```

For example, let's say we have a pandas dataframe df. The following will perform a swifter apply, with the threshold set to 3 seconds
```python
df.swifter.set_dask_threshold(dask_threshold=3).apply(lambda x: x+1)
```

## 10. `pandas.DataFrame.swifter.set_dask_scheduler(scheduler="processes").apply`

Set the dask scheduler

:param scheduler: String, ["threads", "processes"]
```python
def pandas.DataFrame.swifter.set_dask_scheduler(scheduler="processes")
```

For example, let's say we have a pandas dataframe df. The following will perform a swifter apply, with the scheduler set to multithreading.
```python
df.swifter.set_dask_scheduler(scheduler="threads").apply(lambda x: x+1)
```

## 11. `pandas.DataFrame.swifter.allow_dask_on_strings(enable=True).apply`

This flag allows the user to specify whether to allow dask to handle dataframes containing string types. Dask can be particularly slow if you are actually manipulating strings, but if you just have a string column in your data frame this will allow dask to handle the execution.
```python
def pandas.DataFrame.swifter.allow_dask_on_strings(enable=True)
```

For example, let's say we have a pandas dataframe df. The following will allow Dask to process a dataframe with string columns.
```python
df.swifter.allow_dask_on_strings().apply(lambda x: x+1)
```

## 12. `swifter.register_modin()`

This gives access to `modin.DataFrame.swifter.apply(...)` and `modin.Series.swifter.apply(...)`. This registers modin dataframes and series with swifter as accessors.
* NOTE: This is only necessary if you import swifter BEFORE modin. If you import modin before swifter you do not need to execute this method.
