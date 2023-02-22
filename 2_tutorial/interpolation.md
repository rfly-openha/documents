# `interpolation`

Interpolation.

## Syntax

```python
interpolation(x, y, x_est)
interpolation(x, y, x_est, method)
```

## Description

```python
y_est = interpolation(x, y, x_est)
```

The value of the original data at `x_est` is estimated from the input `x`, `y` and the by linear algorithm.

---

```python
y_est = interpolation(x, y, x_est, method)
```

The interpolation method is specifiedd by the argument `method`.

## Examples

```python
>>> from OpenHA.manipulation.preprocess import interpolation
>>> import numpy as np

>>> x = np.array([0, 1, 2, 3])
>>> y = x + np.random.random((4,)) * 0.1
>>> x_est = np.array([1.5, 2.5])
>>> y_est = interpolation(x, y, x_est)
>>> print(x, y)

[0 1 2 3] [0.04362888 1.03800604 2.0397634  3.09172125]

>>> print(y_est)

[1.53888472 2.56574232]

```

---

```python
>>> from OpenHA.manipulation.preprocess import interpolation
>>> import numpy as np

>>> x = np.array([0, 1, 2, 3])
>>> y = x**2 + np.random.random((4,)) * 0.1
>>> x_est = np.array([1.5, 2.5])
>>> y_est = interpolation(x, y, x_est, method='cubic')
>>> print(x, y)

[0 1 2 3] [0.03392971 1.08425927 4.08819547 9.0204196 ]

>>> print(y_est)

[2.34360896 6.31485397]

```

## Input Arguments

`x` —— A 1-D array of real value.

---

`y` —— A 1-D array of real values. The length of `y` along the interpolation axis must be equal to the length of `x`.

---

`method` —— Specifies the kind of interpolation as a string or as an integer specifying the order of the spline interpolator to use. The string has to be one of 'linear', 'nearest', 'nearest-up', 'zero', 'slinear', 'quadratic', 'cubic', 'previous', or 'next'. 'zero', 'slinear', 'quadratic' and 'cubic' refer to a spline interpolation of zeroth, first, second or third order; 'previous' and 'next' simply return the previous or next value of the point; 'nearest-up' and 'nearest' differ when interpolating half-integers (e.g. 0.5, 1.5) in that 'nearest-up' rounds up and 'nearest' rounds down. Default is 'linear'.

