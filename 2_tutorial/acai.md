# `acai`

Computes the degree of controllability (DOC) based on the Availability Control Authority Index, namely ACAI, which is proposed by Guang-Xu Du in [1].

## Syntax

```python
acai(bf, fmax, fmin, G)
```

## Description

```python
doc = acai(bf, fmax, fmin, G)
```

Computes the DOC based on ACAI according to the theory and method that are introduced in the paper.

In mathematics, an enclosed space $U$ is defined as

$$
U = \{\mathbf{f}|\mathbf{f}=[\begin{matrix}f_1 &\cdots&f_i&\cdots & f_n\end{matrix}]^\text{T},f_i\in\left[f_{\min},f_{\max}\right]\}
$$

A new space $\Omega$ is also enclosed, which is defined as

$$
\Omega = \{\mathbf{u}|\mathbf{u}=\mathbf{B}_f\mathbf{f},\mathbf{f}\in U\}
$$

In mathematics, the ACAI is essentially the minimum of the nearest distances between the boundary of $\Omega$ and the given point $\mathbf{G}$.

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

`bf` —— An n-by-m matrix, which refers to the linear map from $U$ to $\Omega$.

For the DOC assessment of the quancopter's propulsion system, it is just the 4-by-m control allocation matrix $\mathbf{b}_f$.

$$
\left[\begin{matrix}\tau_x\\\tau_y\\\tau_z\\ f\end{matrix}\right]
=\mathbf{b}_f\left[\begin{matrix}f_1\\f_2\\\vdots\\ f_n\end{matrix}\right]
$$

where $f_1,f_2,\cdots,f_n$ are the propeller thrusts.

---

`fmax` —— The upper bound of each dimension of the space $U$, specified as a numeric scalar or an array of length `m`.

When the upper bounds of all the dimensions of $U$ are equal, specify it as a numeric scalar.
Otherwise, specify it as an array of numeric scalars of length `m`.

---

`fmin` —— The lower bound of each dimension of the space $U$, specified as a numeric scalar or an array of length `m`.

When the lower bounds of all the dimensions of $U$ are equal, specify it as a numeric scalar.
Otherwise, specify it as an array of numeric scalars of length `m`.

The values of `fmin` should be no more than `fmax`.

---

`G` —— An point in $\Omega$, specified as a 1-D array of length `n`.

## Properties of Arguments

| Name of the parameters | Is optional? | Source, dialog or input port? |
| :--------------------: | :----------: | :---------------------------: |
|          `bf`          |      No      |          Input port           |
|         `fmax`         |      No      |          Input port           |
|         `fmin`         |      No      |          Input port           |
|          `G`           |      No      |          Input port           |

## References

[1] G.-X. Du, Q. Quan, B. Yang, and K.-Y. Cai, "Controllability Analysis for Multirotor Helicopter Rotor Degradation and Failure," Journal of Guidance, Control, and Dynamics, vol. 38, no. 5, pp. 978-984, 2015. DOI: 10.2514/1.G000731.
