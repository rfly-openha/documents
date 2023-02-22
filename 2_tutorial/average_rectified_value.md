# `average_rectified_value`

Compute the average rectified value.

## Syntax

```python
average_rectified_value(x)
```

## Description

```python
m = average_rectified_value(x)
```

In electrical engineering, the average rectified value of a quantity is the average of its absolute value.

$$
\frac{1}{n}\sum_{i=1}^n\left|x_i\right|
$$

## Examples

```python
>>> from OpenHA.manipulation.feature import average_rectified_value
>>> import numpy as np

>>> x = np.array([0, 1, 2, 3, 4])
>>> print(average_rectified_value(x))

2.0

```

## Input Arguments

`x` —— Samples of a quantity.
