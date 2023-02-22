# `variance`

Compute the variance.

## Syntax

```python
variance(x, k)
```

## Description

```python
m = variance(x, k)
```

Returns the variance of the array elements, a measure of the spread of a distribution.

$$
\sigma^2=\frac{1}{n-1}\sum_{i=1}^n \left(x_i-\mu\right)^2
$$

## Examples

```python
>>> from OpenHA.manipulation.feature import variance
>>> import numpy as np

>>> x = np.array([0, 1, 2, 3, 4])
>>> print(variance(x))

2.5

```

## Input Arguments

`x` —— np.ndarray, whose shape is (n, m), refer to `n` samples and the length of each is `m`.
