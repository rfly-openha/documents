# `doc_disturbance_rejection_kang`

## Syntax

```python
doc_disturbance_rejection_kang(A, B, D, Sw)
```

## Description

```python
rho = doc_disturbance_rejection_kang(A, B, D, Sw)
```

This function is used to compute the new measure representing degree of controllability for disturbance rejection.

For the following LTI system

$$
\dot{\mathbf{x}} = \mathbf{A}\mathbf{x}\left(t\right)+\mathbf{B}\mathbf{u}\left(t\right)+\mathbf{D}\mathbf{w}\left(t\right)
$$

where $\mathbf{w}\left(t\right)$ is the disturbance vector.
The disturbance is assumed to be Gaussian white noise with the known correlation
function.
Its Covariance matrix is $\mathbf{S}_w$.

A new measure representing degree of controllability for disturbance rejection in presented in [1].

The controllability Grammian of the system can be calculated by solving the
following differential equation:

$$
\dot{\mathbf{W}}\left(t\right)=\mathbf{A}\mathbf{W}\left(t\right)+\mathbf{W}\left(t\right)\mathbf{A}'+\mathbf{B}\mathbf{B}'
$$

Similarly, the disturbance-sensitivity Grammian satisfies the following differential equation:

$$
\dot{\mathbf{\Sigma}}\left(t\right)=\mathbf{A}\mathbf{\Sigma}\left(t\right)+\mathbf{\Sigma}\left(t\right)\mathbf{A}'+\mathbf{D}\mathbf{S}_w\mathbf{D}'
$$

Then,

$$
\rho = \mathbf{tr}\left\{\mathbf{W}\left(T\right)^{-1}\cdot\mathbf{\Sigma}\left(T\right)\right\}
$$

To eliminate this dependency of the measure on $T$, consider steady-state solutions of Eqs. (5) and (6), satisfying Eqs. (16) and (17) in [1] for asymptotically stable systems:

$$
\begin{aligned}
\mathbf{A}\bar{\mathbf{W}}+\bar{\mathbf{W}}\mathbf{A}'+\mathbf{B}\mathbf{B}'&=0\\
\mathbf{A}\bar{\mathbf{\Sigma}}+\bar{\mathbf{\Sigma}}\mathbf{A}'+\mathbf{D}\mathbf{S}_{\omega}\mathbf{D}'&=0
\end{aligned}
$$

Then

$$
\rho = \mathbf{tr}\left\{\bar{\mathbf{W}}^{-1}\cdot\bar{\mathbf{\Sigma}}\right\}
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

5.999999999999998

```

## Input Arguments

`A` —— System transition matrix of the state-space model of an LTI system, specified as an n-by-n square matrix.

---

`B` —— Input coefficient matrix of the state-space model of an LIT system, specified as an n-by-r matrix.

---

`D` —— Disturbance matrix, specified as an n-by-l matrix.

---

`Sw` —— Covariance matrix of disturbance vectors, specified as an l-by-l square matrix.

## Properties of Arguments

| Name of the parameters | Is optional? | Source, dialog or input port? |
| :--------------------: | :----------: | :---------------------------: |
|          `A`           |      No      |          Input port           |
|          `B`           |      No      |          Input port           |
|          `D`           |      No      |          Input port           |
|          `Sw`          |      No      |          Input port           |

## References

[1] O. Kang, Y. Park, Y. S. Park, M. Suh, "New measure representing degree of controllability for disturbance rejection," Journal of Guidance, Control, and Dynamics, vol. 32, no. 5, pp. 1658-1661, 2009. DOI: 10.2514/1.43864.
