# `trapezoidal_membership_func`

## Syntax

```python
trapezoidal_membership_func((a, b, c, d), x)
```

## Description

```python
r = trapezoidal_membership_func((a, b, c, d), x)
```

This function returns the degree of membership of the state `x` by the trapezoidal membership function, which is determined by the first argument `(a, b, c, d)`.

## Examples

```python
>>> a = 9.8
>>> c = 9.95
>>> d = 10.05
>>> b = 10.2
>>> x = 10.10
# construct the membership function
>>> r = trapezoidal_membership_func((a, b, c, d), x)

0.6666666666666706

```

## Input Arguments

`params` —— A tuple of 4 scalars, the parameters of the trapezoidal membership function.

A four-element-tuple `(a, b, c, d)` is expected, and `a <= b <= c <= d`.
They are the coordinates of the four vertces of the trapezoid from left to right along x-axis.

---

`x` —— A certain system state.
