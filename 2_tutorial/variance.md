# `variance`

Calculates the variance.

## Syntax

```python
variance(x, k)
```

## Description

```python
m = variance(x, k)
```

Calculates the variance of all the observations.

That is

$$
\sigma^2=\frac{1}{n-1}\sum_{i=1}^n \left(x_i-\bar{x}\right)^2
$$

where $x_i,i=1,2,\cdots,n$ represents the $i$-th observed value, and

$$
\bar{x}=\frac{1}{n}\sum_i^n x_i
$$

$\sigma$ is the unbiased estimate of the standard deviation.

## Examples

```python
>>> from OpenHA.processing.feature import variance
>>> import numpy as np

>>> x = np.array([0, 1, 2, 3, 4])
>>> print(variance(x))

2.5

```

## Input Arguments

`x` —— A N-D array of observations.

For an n-by-m array, it indicates `n` observations with `m` features.

## Properties of Arguments

| Name of the parameters | Is optional? | Source, dialog or input port? |
| :--------------------: | :----------: | :---------------------------: |
|          `x`           |      No      |          Input port           |
