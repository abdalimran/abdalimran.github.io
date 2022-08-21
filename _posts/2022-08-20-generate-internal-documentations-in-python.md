---
layout: post
title: Generate internal documentation of functions and attributes in Python Modules
category: 
    - "Python"
---
Nobody can memorize and remember all the functions offered by Python in its numerous modules. 
That's why while coding in Python we always refer to in google and read the documentation.
But what if there was no google? Can we retrive the internal documentations that come with Python by default?
Yes, we can do it. I've written the following function to generate internal documentation table of any python module.
This function requires `pandas` package. If it's not installed in your system please use `pip install pandas` to install it.

```python
import pandas as pd
pd.set_option('display.max_rows', 500)

def get_default_documentation(modl):
  documentation_dict = dict(
                              zip(
                                [i for i in dir(modl)], 
                                zip(
                                    ['function' if callable(getattr(modl, i)) else 'attribute' for i in dir(modl)],
                                    [getattr(modl, i).__doc__ for i in dir(modl)],
                                )
                              )
                          )
  documentation = pd.DataFrame(documentation_dict)\
                              .transpose()\
                              .rename_axis('name')\
                              .rename(columns={0:'type', 1:'documentation'})\
                              .sort_index()\
                              .sort_values(by='type')

  documentation = documentation.style.set_properties(**{'text-align': 'left'})
  
  return documentation
```

Now you can call the `get_default_documentation` and pass the module name for which you want to generate the internal documentation table.

**For Example:**
```python
get_default_documentation(str)
```

You can get the full list of Python Libraries from this link: [https://docs.python.org/3.7/py-modindex.html](https://docs.python.org/3.7/py-modindex.html)
This function will also work on thrid-party libraries.
