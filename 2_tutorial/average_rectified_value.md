# `average_rectified_value`

Calculates the average rectified value.

## Syntax

```python
average_rectified_value(x)
```

## Description

```python
m = average_rectified_value(x)
```

In electrical engineering, the average rectified value is the average of its absolute value.

That is,

$$
X_\text{ARV} = \frac{1}{n}\sum_{i=1}^n\left|x_i\right|
$$

where $x_i,i=1,2,\cdots,n$ represents the $i$-th observed value.

## Examples

```python
>>> from OpenHA.processing.feature import average_rectified_value
>>> import numpy as np

>>> x = np.array([0, 1, 2, 3, 4])
>>> print(average_rectified_value(x))

2.0

```

## Input Arguments

`x` —— A 1-D array of observations of length `n`, namely `n` observations of a quantity.
