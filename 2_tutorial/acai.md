# `acai`

Compute the degree of controllability (DoC) based on the Availability Control Authority Index, namely ACAI, which is propused by Guang-Xu Du in his paper [1].

## Syntax

```python
acai(bf, fmax, fmin, G)
```

## Description

```python
doc = acai(bf, fmax, fmin, G)
```

Returns the DoC based on ACAI according to computation method that is introduced in the paper.

The mathematical essence of ACAI is the minimum of the nearest distance between the boundary of a closed space with boundaries `fmax` and `fmin` and the boundary of the new space obtained by mapping the matrix `bf` to its interior point `G`.

## Examples

```python
>>> from OpenHA.assessment.attribute import acai, control_allocation
>>> import numpy as np

>>> bf = control_allocation(4, 0.28, 0.1)
>>> fmax, fmin = 6, 0
>>> G = np.array([15, 0, 0, 0]).reshape((-1, 1))
>>> acai(bf, fmax, fmin, G)

0.7299473938200366

```

## Input Arguments

`bf` —— An m-by-n matrix, which is refer to the linear reflection from the original space to the new one.

For the DoC assessment of propulsion system of a multicopter, `bf` is just the control allocation matrix.

$$
\left[\begin{matrix}\tau_x\\\tau_y\\\tau_z\\f\end{matrix}\right]
=\mathbf{b}_f\left[\begin{matrix}f_1\\f_2\\\vdots\\f_n\end{matrix}\right]
$$

where $f_1,f_2,\cdots,f_n$ are the force that produced by each propeller.

---

`fmax` —— The upper boundary of the original space.

If it's a scalar, it determines the maximum value of each element of the space vector, namely $\left[0,f_{\max}\right]$.

If it's a vector of the length `n`, its elements determine the maximum value of each corresponding element of the space vector.

---

`fmin` —— The lower boundary of the original space.

If it's a scalar, it determines the minmum value of each element of the space vector, namely $\left[0,f_{\min}\right]$.

If it's a vector of the length `n`, its elements determine the minmum value of each corresponding element of the space vector.

---

`G` —— An numpy array, whose shape is `(n, 1)`.

## References

[1] G.-X. Du, Q. Quan, B. Yang, and K.-Y. Cai, "Controllability Analysis for Multirotor Helicopter Rotor Degradation and Failure," Journal of Guidance, Control, and Dynamics, vol. 38, no. 5, pp. 978-984, 2015. DOI: 10.2514/1.G000731.
