# `central_moment`

Compute the central moment.

## Syntax

```python
central_moment(x, k)
```

## Description

```python
m = central_moment(x, k)
```

Compute the k-th central moment of the timeseries `x`, whose length is `n`.

$$
\frac{1}{n}\sum_{i=1}^n\left(x_i-\bar{x}\right)^k
$$

## Examples

```python
>>> from OpenHA.manipulation.feature import central_moment
>>> import numpy as np

>>> x = np.array([0, 1, 2, 3, 4])
>>> print(central_moment(x, 2))

2

```

## Input Arguments

`x` —— Samples of a signal, whose shape is `(n, m)`, refer to `n` samples and the length of each is `m`.

---

`k` —— The number of the order.
