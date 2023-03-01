# `doc_gramian`

## Syntax

```python
doc_gramian(A, B)
```

Compute the Gramian-matrix-based DOC.

## Description

```python
rho1, rho2, rho3 = doc_gramian(A, B)
```

Computes the Gramian-matrix-based DOC of an LTI system, which refers to equation (2.9) in the paper [1].
The mathematical principle is available in Section 2.2 of [2].

$$
\begin{aligned}
\dot{\mathbf{x}}&=\mathbf{A}\left(t\right)\mathbf{x}+\mathbf{B}\left(t\right)\mathbf{u}\\
\mathbf{y}&=\mathbf{C}\left(t\right)\mathbf{x}
\end{aligned}
$$

For the above linear time-variant system, we recall the relation of the controllability problem to the fixed-time minimum-energy transfer control problem.

$$
J\left(t_1,t_0;\mathbf{x}_0\right)=\min_{\mathbf{u}}\int_{t_0}^{t_1}\left\|\mathbf{u}\left(\tau\right)\right\|^2\text{d}\tau\\
\mathbf{x}\left(t_0\right)=\mathbf{x}_0,\mathbf{x}\left(t_1\right)=0
$$

The optimization problem is solved for each initial condition $x_0$ if and only if the system is completely controllable at $\left[t_0,t_1\right]$.
Then the minimum control energy is given by

$$
J\left(t_1,t_0;\mathbf{x}_0\right)=\mathbf{x}_0^{\text{T}}\mathbf{W}_c^{-1}\left(t_1,t_0\right)\mathbf{x}_0
$$

where $\mathbf{W}_c$ a kind of the controllability matrix associated with $\mathbf{A}\left(t\right)$ and $\mathbf{B}\left(t\right)$.

Then the minimum eigenvalue, trace, and determinant of the $\mathbf{W}_c^{-1}\left(t_1,t_0\right)$ are just three proper physically meaningful measures of the quality of controllability.

- $\lambda_{\min}\left(\mathbf{W}_c\right)$. Related to the maximum value of the minimum control energy over the unit ball $\left\{\mathbf{x}_0:\left\|\mathbf{x}_0\right\|=1\right\}$.
- $\frac{n}{\text{tr}\mathbf{W}_c^{-1}}$. Related to the average value of the minimum control energy over the unit hypersphere $\left\{\mathbf{x}_0:\left\|\mathbf{x}_0\right\|=1\right\}$.
- $\text{det}\mathbf{W}_c$. A characteristic of the attainable set of initial state vectors with prescribed maximum costs.

For the special case of an LTI system, the controllability matrix is

$$
\mathbf{Q}=\left[\begin{matrix}
\mathbf{B}&\mathbf{A}\mathbf{B}&\mathbf{A}^2\mathbf{B}&\cdots&\mathbf{A}^{p-1}\mathbf{B}
\end{matrix}\right]
$$

The three above measures become

$$
\begin{aligned}
\rho_1&=\lambda_{\min}\left(\mathbf{Q}^{\text{T}}\mathbf{Q}\right)\\
\rho_2&=\frac{n}{\text{tr}\left\{\left(\mathbf{Q}^{\text{T}}\mathbf{Q}\right)^{-1}\right\}}\\
\rho_3&=\sqrt[n]{\left(\mathbf{Q}^{\text{T}}\mathbf{Q}\right)}
\end{aligned}
$$

Significantly, this function is only for LTI systems.

## Examples

```python
>>> from OpenHA.assessment.attribute import doc_gramian
>>> import numpy as np

>>> A = np.array(
        [
            [0, 1, 0, 0, 0],
            [0, -0.089, 0.7132, 0, 0.8903],
            [0, 0, 0, 1, 0],
            [0, -0.2671, 31.5391, 0, 2.6708],
            [0, 0, 0, 0, -1],
        ]
    )
>>> B = np.array([0, 0, 0, 0, -1]).reshape((-1, 1))
>>> doc_gramian(A, B)

(0.204458903592688, 0.707999248988378, 29.896138372000475)

```

## Input Arguments

`A` —— System transition matrix of the state-space model of an LTI system, specified as an n-by-n square matrix.

---

`B` —— Input coefficient matrix of the state-space model of an LIT system, specified as an n-by-p matrix.

## Output Arguments

A tuple `(rho1, rho2, rho3)`, whose physical meanings are introduced above.

---

## References

[1] G.-X. Du, Q. Quan, "Degree of Controllability and its Application in Aircraft Flight Control," Journal of Systems Science and Mathematical Sciences, vol. 34, no. 12, pp. 1578-1594, 2014.

[2] P.C. Müller, H.I. Weber, "Analysis and optimization of certain qualities of controllability and observability for linear dynamical systems," vol. 8, no. 3, pp. 237-246, 1972. DOI: 10.1016/0005-1098(72)90044-1.
