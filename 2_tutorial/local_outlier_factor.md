# `local_outlier_factor`

## Syntax

```python
local_outlier_factor(points, k)
```

## Description

```python
lof = local_outlier_factor(points, k)
```

The Local Outlier Factor (LOF) of all the points are computed.
And the LOF is an algorithm used for outlier detection, which is proposed by Breunig in [1].

## Examples

```python
>>> from OpenHA.manipulation.preprocess import local_outlier_factor
>>> import numpy as np

>>> points = np.array([0, 1, 1.2, 2, 3, 10])
>>> print(local_outlier_factor(points, 3))

[1.01666667 1.01666667 0.95238095 0.975      1.16190476 5.525     ]

```

## Input Arguments

`points` —— An array of vectors of length `n`, namely `n` points, specified as an N-D array.

---

`k` —— Number of neighbors for k-distance and k-neighbors, specified as a positive integer scalar.

## References

[1] M. M. Breunig, H.-P. Kriegel, R. T, Y. Ng, J. Sander. "LOF: Identifying Density-Based Local Outliers." Proceedings of the 2000 ACM SIGMOD International Conference on Management of Data, 2000, pp. 93–104. DOI: 10.1145/342009.335388.
