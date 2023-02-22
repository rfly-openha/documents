# `doc_disturbance_rejection_kang`

## Syntax

```python
doc_disturbance_rejection_kang(A, B, D, Sw)
```

## Description

```python
rho = doc_disturbance_rejection_kang(A, B, D, Sw)
```

This method is used to calculate the controllability of an LTI system to reject disturbances.

$$
\dot{\mathbf{x}} = \mathbf{A}\mathbf{x}+\mathbf{B}\mathbf{u}+\mathbf{D}\mathbf{\omega}
$$

where $\omega$ is a disturbance with covariance `Sw`.

A new measure representing degree of controllability for disturbance rejection in presented in [1].

Specifically, a method is given for calculating this DoC for a general system.

For LTI systems, it is proven that the differential equation is equivalent to the lyapunov equation.

$$
\begin{aligned}
\mathbf{A}\bar{\mathbf{W}}+\bar{\mathbf{W}}\mathbf{A}'+\mathbf{B}\mathbf{B}'&=0\\
\mathbf{A}\bar{\mathbf{\Sigma}}+\bar{\mathbf{\Sigma}}\mathbf{A}'+\mathbf{D}\mathbf{S}_{\omega}\mathbf{D}'&=0
\end{aligned}
$$

Then

$$
\rho = \mathbf{tr}\left\{\bar{\mathbf{\Sigma}}\cdot\bar{\mathbf{W}}^{-1}\right\}
$$

Details of the proof and other details can be found in the original literature.

## Examples

```python
>>> from OpenHA.assessment.attribute import doc_disturbance_rejection_kang
>>> import numpy as np

>>> A = np.array(
        [
            [0, 0, 0, 1, 0, 0],
            [0, 0, 0, 0, 1, 0],
            [0, 0, 0, 0, 0, 1],
            [-2, 1, 0, -2, 1, 0],
            [1, -2, 1, 1, -2, 1],
            [0, 1, -1, 0, 1, -1],
        ]
    )
>>> B = np.array([[0, 0, 0, 0, 1, 0]]).T
>>> D = np.array([[0, 0, 0, 0, 1, 0]]).T
>>> Sw = np.array([[1]])

>>> doc_disturbance_rejection_kang(A, B, D, Sw)

6.000000000000201

```

## Input Arguments

`A` —— State matrix of the state space equation, which is n-by-n.

---

`B` —— Input matrix of the state space equation, which is n-by-p.

---

`D` —— Matrix with proper dimension.

---

`Sw` —— Covariance matrix of disturbance vector $\omega$, with proper dimension.

## References

[1] O. Kang, Y. Park, Y. S. Park, M. Suh, "New measure representing degree of controllability for disturbance rejection," Journal of Guidance, Control, and Dynamics, vol. 32, no. 5, pp. 1658-1661, 2009. DOI: 10.2514/1.43864.
