# `local_outlier_factor`

## Syntax

```python
local_outlier_factor(points, k)
```

## Description

```python
lof = local_outlier_factor(points, k)
```

The local outlier factor algorithm

Detect outliers by the local outlier factor.

## Examples

```python
>>> from OpenHA.manipulation.preprocess import local_outlier_factor
>>> import numpy as np

>>> points = np.array([0, 1, 1.2, 2, 3, 10])
>>> print(local_outlier_factor(points, 3))

[1.01666667 1.01666667 0.95238095 0.975      1.16190476 5.525     ]

```

## Input Arguments

`points` —— Specified as a numeric matrix. Each row of X corresponds to one observation, and each column corresponds to one predictor variable.

---

`k` —— Number of nearest neighbors in the `points` to find for computing the local outlier factor values, specified as a positive integer value.

## References

[1] Breunig, Markus M., et al. "LOF: Identifying Density-Based Local Outliers." Proceedings of the 2000 ACM SIGMOD International Conference on Management of Data, 2000, pp. 93–104.
