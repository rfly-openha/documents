# `kurtosis`

Compute the kurtosis of time series.

## Syntax

```python
kurtosis(x, k)
```

## Description

```python
m = kurtosis(x, k)
```

Compute the kurtosis of time series.

$$
\frac{E\left(X-\mu\right)^4}{\sigma^4}
$$

## Examples

```python
>>> from OpenHA.manipulation.feature import kurtosis
>>> import numpy as np

>>> x = np.array([0, 1, 2, 3, 4])
>>> print(kurtosis(x))

1.088

```

## Input Arguments

`x` —— `n` samples of times series.
