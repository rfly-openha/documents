# `bay_set_model`

Load the original D matrix data and train the model of bayesian network.

## Syntax

```python
bay_set_model(path, model_path)
```

## Description

By using this function, input the D matrix data about the test indicators and faults, and this function will call the `BayesianNetwork` class in `pgmpy` to train the bayesian network model, and the model itself will be saved at the `model_path`, which is also an input argument.

## Examples

```python
>>> import panda as pd
>>> import numpy as np
>>> import random
>>> from pgmpy.models import BayesianNetwork

>>> path = <your folder absolute path> + '/' + 'D_matrix.xlsx'
>>> model_path = <your folder absolute path> + '/' + 'model.xmlbif'
>>> bay_set_model(path, model_path)

```
Attention:

The generated pre-trained model will be saved at `model_path`, and an example contains the source D matrix data files and pre-trained models are also uploaded at [Bayesian Net Download](https://rfly-openha.github.io/documents/5_download_support/BayesianNetDownload.html) website. 


## Input Arguments

`path` —— A string. It is the path where the source D matrix data file is located. It is recommended to use the absolute path of this file, for the function doesn't handle the input path exactly.

---

`model_path` —— A string. It is the path where the trained bayesian network will be saved. It is recommended to use the absolute path of this file, for the function doesn't handle the input path exactly.

## Properties of Arguments
| Name of the parameters  | is optional?    | Source, dialog or input port?|
| -------------------- | ------------------------- |---------------------- |
|          `path`         |          No           |        Input port      |
|     `model_path`      |          No           |        Input port        |
