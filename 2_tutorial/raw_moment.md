# `raw_moment`

Calculates the raw moment.

## Syntax

```python
raw_moment(x, k)
```

## Description

```python
m = raw_moment(x, k)
```

Calculates the k-th raw moment of all the observations.

That is,

$$
A_k = \frac{1}{n}\sum_{i=1}^nx_i^k
$$

where $x_i,i=1,2,\cdots,n$ represents the $i$-th observed value.

## Examples

```python
>>> from OpenHA.manipulation.feature import raw_moment
>>> import numpy as np

>>> x = np.array([0, 1, 2, 3, 4])
>>> print(raw_moment(x, 2))

# = (0^2 + 1^2 + 2^2 + 3^2 + 4^2) / 5
# = (0 + 1 + 4 + 9 + 16) / 5
# = 30 / 5
6

```

## Input Arguments

`x` —— A N-D array of observations.

For an n-by-m array, it indicates `n` observations with `m` features.

---

`k` —— Order of raw moment, specified as a positive integer scalar.
