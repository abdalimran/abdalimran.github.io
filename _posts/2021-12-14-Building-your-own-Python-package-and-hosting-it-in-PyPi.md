---
layout: post
title: Building your own Python package and hosting it in PyPi
category: 
    - "Python"
    - "Development"
---

Follow the below steps and run suitable commands.

## Make sure you have upgraded version of pip
Windows
```
python -m pip install --upgrade pip
```

Linux/MAC OS
```
python3 -m pip install --upgrade pip
```

## Create a project with the following structure
```
packaging_tutorial/
├── LICENSE
├── pyproject.toml
├── README.md
├── setup.cfg
├── src/
│   └── example_package/
│       ├── __init__.py
│       └── example.py
└── tests/
```
To produce the above structure you can run the following commands.
```
touch LICENSE
touch pyproject.toml
touch setup.cfg
mkdir src/mypackage
touch src/mypackage/__init__.py
touch src/mypackage/main.py
mkdir tests
```

## pyproject.toml 

This file tells tools like pip and build how to create your project

```
[build-system]
requires = [
    "setuptools>=42",
    "wheel"
]
build-backend = "setuptools.build_meta"
```
build-system.requires gives a list of packages that are needed to build your package. Listing something here will only make it available during the build, not after it is installed.

build-system.build-backend is the name of Python object that will be used to perform the build. If you were to use a different build system, such as flit or poetry, those would go here, and the configuration details would be completely different than the setuptools configuration described below.


## Setup.cfg setup
Using `setup.cfg` is a best practice, but you could have a dynamic setup file using `setup.py`

```
[metadata]
name = example-pkg-YOUR-USERNAME-HERE
version = 0.0.1
author = Example Author
author_email = author@example.com
description = A small example package
long_description = file: README.md
long_description_content_type = text/markdown
url = https://github.com/pypa/sampleproject
project_urls =
    Bug Tracker = https://github.com/pypa/sampleproject/issues
classifiers =
    Programming Language :: Python :: 3
    License :: OSI Approved :: MIT License
    Operating System :: OS Independent

[options]
packages = find:
python_requires = >=3.7
include_package_data = True
```
## Running the build
### Make sure your build tool is up to date
Windows
```
python -m pip install --upgrade build
```
Linux/MAC OS
```
python3 -m pip install --upgrade build
```


### Create the build
```
python -m build
```

## Uploading the distribution archives to test PyPi
```
python3 -m pip install --upgrade twine
python3 -m twine upload --repository testpypi dist/*
```

### Installing your newly uploaded package from test PyPi
```
python3 -m pip install --index-url https://test.pypi.org/simple/ --no-deps example-pkg-YOUR-USERNAME-HERE
```

## Uploading the distribution archives to real PyPi
Use `twine upload dist/*` to upload your package and enter your credentials for the account you registered on the real PyPI. Now that you’re uploading the package in production, you don’t need to specify `--repository`; the package will upload to https://pypi.org/ by default.

## References
https://packaging.python.org/tutorials/packaging-projects/
