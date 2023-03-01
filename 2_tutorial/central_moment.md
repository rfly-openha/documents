# `central_moment`

Calculates the central moment.

## Syntax

```python
central_moment(x, k)
```

## Description

```python
m = central_moment(x, k)
```

Compute the k-th central moment of all the observations.

That is,

$$
B_k = \frac{1}{n}\sum_{i=1}^n\left(x_i-\bar{x}\right)^k
$$

where $x_i,i=1,2,\cdots,n$ represents the $i$-th observed value, and

$$
\bar{x}=\frac{1}{n}\sum_i^n x_i
$$

## Examples

```python
>>> from OpenHA.manipulation.feature import central_moment
>>> import numpy as np

>>> x = np.array([0, 1, 2, 3, 4])
>>> print(central_moment(x, 2))

# x_ = 2
# = ((-2)^2 + 1^2 + 0^2 + 1^2 + 2^2) / 5
# = (4 + 1 + 0 + 1 + 4) / 5
# = 10 / 5
2

```

## Input Arguments

`x` —— A N-D array of observations.

For an n-by-m array, it indicates `n` observations with `m` features.

---

`k` —— Order of raw moment, specified as a positive integer scalar.
