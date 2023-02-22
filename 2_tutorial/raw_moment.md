# `raw_moment`

Compute the raw moment.

## Syntax

```python
raw_moment(x, k)
```

## Description

```python
m = raw_moment(x, k)
```

Compute the k-th raw moment of the timeseries `x`, whose length is `n`.

$$
\frac{1}{n}\sum_{i=1}^nx_i^k
$$

## Examples

```python
>>> from OpenHA.manipulation.feature import raw_moment
>>> import numpy as np

>>> x = np.array([0, 1, 2, 3, 4])
>>> print(raw_moment(x, 2))

6

```

## Input Arguments

`x` —— Samples of a signal, whose shape is `(n, m)`, refer to `n` samples and the length of each is `m`.

---

`k` —— The number of the order.
