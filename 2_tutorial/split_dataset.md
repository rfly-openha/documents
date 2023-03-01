# `split_dataset`

Split the dataset into train and test subsets randomly.

## Syntax

```python
split_dataset(X, Y)
split_dataset(X, Y, percent)
```

## Description

```python
X1, Y1, X2, Y2 = split_dataset(X, Y)
```

Split the dataset with features `X` and labels `Y` into `X1, X2, Y1, Y2` randomly.
The order of the features and their corresponding labels remain unchanged.
The proportion of the dataset `X` to include in the train split `X1` is 15% as default.

It's similar to the function [`sklearn.model_selection.train_test_split`](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html).

---

```python
X1, Y1, X2, Y2 = split_dataset(X, Y, percent)
```

The proportion of the dataset `X` to include in the train split `X1` is specified by `percent`.

## Examples

```python
>>> from OpenHA.core import split_dataset
>>> import numpy as np

>>> X = np.random.randint(0, 10, size=(10, 3))
>>> Y = np.random.randint(0, 2, size=(10,))
>>> X, Y

(array([[2, 4, 8],
        [9, 5, 2],
        [2, 0, 2],
        [1, 2, 8],
        [9, 8, 3],
        [8, 5, 6],
        [6, 9, 9],
        [8, 7, 4],
        [4, 3, 9],
        [2, 5, 3]]),
 array([0, 0, 0, 1, 0, 0, 1, 1, 0, 0]))

>>> X1, Y1, X2, Y2 = split_dataset(X.tolist(), Y.tolist(), percent=0.3)
>>> X1, Y1, X2, Y2

([[9, 5, 2], [1, 2, 8], [8, 7, 4]],
 [0, 1, 1],
 [[2, 4, 8], [2, 0, 2], [9, 8, 3], [8, 5, 6], [6, 9, 9], [4, 3, 9], [2, 5, 3]],
 [0, 0, 0, 0, 1, 0, 0])

```

## Input Arguments

`X` —— Feature vectors, specified as an array of vectors of length `n`.

---

`Y` —— Labels, specified as an array of vectors of numeric scalars of length `n`.

---

`percent` —— The proportion of the dataset `X` to include in the train split `X1`, specified as a positive float number in $\left[0,1\right]$.

## Output Arguments

A tuple `(X1, Y1, X2, Y2)`.
