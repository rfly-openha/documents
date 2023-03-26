# `doc_recovery_region`

Computes the DOC based on the recovery region.

## Syntax

```python
doc_recovery_region(A, B, U, T, N)
```

## Description

```python
doc = doc_recovery_region(A, B, U, T, N)
```

The DOC based on the recovery region is returned by this function.
The computation method is illustrated in [1] and [2].

For an LTI system as follows.

$$
\dot{\mathbf{x}}\left(t\right) = \mathbf{A}\mathbf{x}\left(t\right)+\mathbf{B}\mathbf{u}\left(t\right)
$$

The recovery region for time $T$ for the above system is the set

$$
R=\left\{\mathbf{x}\left(0\right)|\exists\mathbf{u}\left(t\right)\in U,t\in\left[0,T\right],\mathbf{x}\left(T\right)=0\right\}
$$

where $U$ is a bounded closed space.

The DOC in time $T$ of the $\mathbf{x}=0$ is defined as

$$
\rho=\inf\left\|\mathbf{x}\left(0\right)\right\|,\forall \mathbf{x}\left(0\right)\notin R
$$

A new conservative approximation technique has been developed for estimating the degree of controllability of general LTI systems.
The procedure involves discretization of the continuous system and computation of
the degree of controllability of the resulting discrete system.
More details are available in [1] [2].

The parameter `A` and `B` are the state matrix and input matrix of the state-space model, respectively.
`T` specifies the recovery time, and `N` is the number of intervals for discretization.
`U` specifies the minimum and maximum values of the control inputs.

## Examples

```python
>>> from OpenHA.assessment.attribute import doc_recovery_region,control_allocation
>>> import numpy as np
>>> A = np.concatenate(
        (np.concatenate((np.zeros((3, 3)), np.eye(3)), axis=1), np.zeros((3, 6))), axis=0
    )
>>> Bf = control_allocation(6, 0.28, 0.1, giveup_height=True)
>>> B = np.matmul(
        np.concatenate(
            (np.zeros((3, 3)), np.diag([1 / 0.0411, 1 / 0.0478, 1 / 0.0599])), axis=0
        ),
        Bf,
    )
>>> doc_recovery_region(A, B, (0, 6), 0.4, 2)

2.0004666531792434

```

## Input Arguments

`A` —— System transition matrix of the state-space model of an LTI system, specified as an n-by-n square matrix.

---

`B` —— Input coefficient matrix of the state-space model of an LTI system, specified as an n-by-p matrix.

---

`U` —— The minimum and maximum values of the control inputs, specified as a tuple `(fmin, fax)`.
See [acai](./acai.html/#input-arguments) for more information.

---

`T` —— Recovery time, specified as a positive numeric scalar.

---

`N` —— The number of intervals for discretization, specified as a positive integer scalar.

`dt=T/N` is the sample time.

## Properties of Arguments

| Name of the parameters | Is optional? | Source, dialog or input port? |
| :--------------------: | :----------: | :---------------------------: |
|          `A`           |      No      |          Input port           |
|          `B`           |      No      |          Input port           |
|          `U`           |      No      |          Input port           |
|          `T`           |      No      |          Input port           |
|          `N`           |      No      |          Input port           |

## References

[1] B Yang, G.-X. Du, Q. Quan, K.-Y. Cai, "The Degree of Controllability with Limited Input and an Application for Hexacopter Design," in Proceedings of the 32nd Chinese Control Conference. Xi'an, Shaanxi, China, 2013.

[2] G. Klein, R. E. L. Jr., W. W. Longman, "Computation of a Degree of Controllability Via System Discretization," Journal of Guidance, Control, and Dynamic, vol 5, no. 6, pp. 583-589, 1982. DOI: 10.2514/3.19793
