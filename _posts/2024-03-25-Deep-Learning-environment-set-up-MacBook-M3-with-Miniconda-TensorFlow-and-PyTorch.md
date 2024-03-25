---
layout: post
title: Deep Learning environment set-up MacBook M3 with Miniconda, TensorFlow, and PyTorch
category:
    - "Deep Learning"
    - "Macbook M3"
    - "Miniconda"
    - "TensorFlow"
    - "PyTorch"
    - "GPU"
---
Here is the process of installing TensorFlow and PyTorch on a MacBook with an M3 chip, leveraging Miniconda for a smooth installation experience. Whether you're a data scientist, a machine learning enthusiast, or a developer looking to harness the power of these libraries, this guide will help you set up your environment efficiently.

## Prerequisites

Before we dive into the installation process, ensure your MacBook meets the following requirements:

- macOS 12.3 or later
- Native arm64 version of Python
- Xcode Command Line Tools installed

## Installing Xcode Command Line Tools

First, we need to install Xcode Command Line Tools, which includes compilers and other necessary tools for TensorFlow and PyTorch. Open Terminal and run:

`xcode-select --install`

## Setting Up Miniconda

Miniconda is a minimal installer for conda, a package, dependency, and environment management system. It's lightweight and perfect for our needs.

* Download Miniconda3 macOS M1 64-bit.pkg from the official website (https://docs.conda.io/en/latest/miniconda.html).
* Open the downloaded file and follow the installation instructions.

## Creating a Conda Environment

It's a good practice to create a separate environment for TensorFlow and PyTorch to avoid conflicts between dependencies.

Create a new environment named `deeplearning-env`:

`conda create -n deeplearning-env python=3.10.13`

Activate the environment:

`conda activate deeplearning-env`

## Installing TensorFlow

With the environment activated, we can now install TensorFlow and its dependencies.

Install TensorFlow dependencies:

`conda install -c apple tensorflow-deps`

Install TensorFlow for macOS:

`pip install tensorflow-macos`

Install the Metal plugin for GPU support:

`pip install tensorflow-metal`

## Verifying Tensorflow Installation

To ensure everything is set up correctly, we'll verify the installation and check if the GPU is available for TensorFlow and PyTorch.

For TensorFlow, run:

```python
import sys
import keras
import tensorflow as tf
import platform

print(f"Python Platform: {platform.platform()}")
print(f"Tensor Flow Version: {tf.__version__}")
print(f"Keras Version: {keras.__version__}")
gpu = len(tf.config.list_physical_devices("GPU")) > 0
print("GPU is", "available" if gpu else "NOT AVAILABLE")
```

## Installing PyTorch

Now, let's install PyTorch.

Visit the PyTorch getting started page and select the appropriate options for your system. For a MacBook with an M3 chip, you should choose Preview (Nightly) for MPS device acceleration. Then, run the provided pip command, for example:

`pip3 install torch torchvision torchaudio`

## Verifying PyTorch Installation

Start a Jupyter notebook and run the following code to verify PyTorch installation and MPS availability:

```python
import torch
print(f"PyTorch version: {torch.__version__}")
print(f"Is MPS (Metal Performance Shader) built? {torch.backends.mps.is_built()}")
print(f"Is MPS available? {torch.backends.mps.is_available()}")
device = "mps" if torch.backends.mps.is_available() else "cpu"
print(f"Using device: {device}")
```

**Run PyTorch on MPS**: To utilize the MPS backend for GPU acceleration, set the device to "mps" when creating tensors or models:

```python
device = "mps" if torch.backends.mps.is_available() else "cpu"
x = torch.rand(size=(3, 4)).to(device)
```

By following these steps, you should have PyTorch installed and configured to leverage the GPU on your MacBook with an M3 chip, enabling accelerated training and inference for machine learning models

**What is Metal Performance Shader?**

Metal Performance Shaders are particularly useful for machine learning tasks, as they enable high-performance training and inference on the GPU. This is supported by various machine learning frameworks such as PyTorch, TensorFlow, and JAX, which have backends for Metal. These frameworks can leverage Metal Performance Shaders to run operations on the GPU, taking advantage of the compute performance of Apple Silicon GPUs.

For example, PyTorch operations can be implemented as custom Metal shaders or using Apple's own collection of Metal shaders included in the Metal Performance Shaders framework. This allows for operations like matrix multiplication to be performed on the GPU cores. This integration facilitates the execution of machine learning models on Apple Silicon GPUs, potentially offering performance benefits over other compute subsystems like the Apple Neural Engine (ANE)
