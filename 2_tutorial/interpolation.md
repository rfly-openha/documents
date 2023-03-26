# `interpolation`

Interpolation.

## Syntax

```python
interpolation(x, y, x_est)
interpolation(x, y, x_est, kind)
```

## Description

```python
y_est = interpolation(x, y, x_est)
```

`x` and `y` are arrays of values used to approximate some function `f: y = f(x)`.
This function returns an array of the interpolated values at `x_est` by linear interpolation as default.

---

```python
y_est = interpolation(x, y, x_est, kind)
```

The interpolation method is specified by the parameter `kind`.

## Examples

```python
>>> from OpenHA.processing.preprocess import interpolation
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
>>> from OpenHA.processing.preprocess import interpolation
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

`x` —— $x$-coordinates. A 1-D array of real value.

---

`y` —— A N-D array of real values. The length of `y` along the interpolation axis must be equal to the length of `x`.

---

`x_est` —— A 1-D array of values to evaluate the interpolant.

---

`kind` —— Kind of interpolation, specified as one of the following strings.

- `zero`, `slinear`, `quadratic` and `cubic` refer to a spline interpolation of zeroth, first, second or third order.
- `previous` and `next` simply return the previous or next value of the point.
- `nearest-up` and `nearest` differ when interpolating half-integers (e.g., 0.5, 1.5) in that `nearest-up` rounds up and `nearest` rounds down.

The default is `linear`.

## Properties of Arguments

| Name of the parameters | Is optional? | Source, dialog or input port? |
| :--------------------: | :----------: | :---------------------------: |
|          `x`           |      No      |          Input port           |
|          `y`           |      No      |          Input port           |
|        `x_est`         |      No      |          Input port           |
|         `kind`         |     Yes      |            Dialog             |
