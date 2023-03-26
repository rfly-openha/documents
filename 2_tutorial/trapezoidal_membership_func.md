# `trapezoidal_membership_func`

## Syntax

```python
trapezoidal_membership_func((a, b, c, d), x)
```

## Description

```python
r = trapezoidal_membership_func((a, b, c, d), x)
```

This function returns the degree of membership of the state `x` to a set, whose membership function is trapezoidal.
The shape of the trapezoidal membership function is specified by the `params`, namely `(a, b, c, d)`.
It will be triangular if `b == c`, and rectangular if `a == b` and `c == d`.

The membership function is

$$
f\left(x\right)=\begin{cases}
0&x<a\\
\frac{x-a}{c-a}&a\leqslant x <c\\
1 & c\leqslant x<d\\
\frac{b-x}{b-d}&d\leqslant x <b\\
1 & b\leqslant x

\end{cases}
$$

## Examples

```python
>>> a = 9.8
>>> c = 9.95
>>> d = 10.05
>>> b = 10.2
>>> x = np.linspace(9.8, 10.2, 10)

>>> f = lambda x: trapezoidal_membership_func((a, b, c, d), x)
# construct the membership function
>>> r = f(x)

[0, 0.29629629629629806, 0.5925925925925961, 0.8888888888888942, 1, 1, 0.8888888888888942, 0.5925925925925961, 0.29629629629629806, -0.0]

```

## Input Arguments

`params` —— A tuple `(a, b, c, d)` that specifies the shape of the trapezoidal membership function, and `a <= b <= c <= d`.

---

`x` —— System states, specified as an array of numeric scalars of vectors.

## Properties of Arguments

| Name of the parameters | Is optional? | Source, dialog or input port? |
| :--------------------: | :----------: | :---------------------------: |
|        `params`        |      No      |            Dialog             |
|          `x`           |      No      |          Input port           |
