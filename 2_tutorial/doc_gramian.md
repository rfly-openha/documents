# `doc_gramian`

## Syntax

```python
doc_gramian(A, B)
```

Compute the Gramian-matrix-based DoC.

## Description

```python
rho1, rho2, rho3 = doc_gramian(A, B)
```

Returns the DoC, which refers to equation (2.9) in the paper [1].

The method incorporates three different DoCs, depending on the energy optimisation objective.

Significantly, it's only works for LTI systems.

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

`A` —— State matrix of the state space equation, which is n-by-n.

---

`B` —— Input matrix of the state space equation, which is n-by-p.

## Output Arguments

`rho1` —— The DoC based on the maxmum of the minmun energy that is needed to drive the state point from any of the initial sphere to origin.

---

`rho2` —— The DoC based on the average energy that is needed to drive the state point from any of the initial sphere to origin.

---

`rho3` —— The DoC based on the maximum range of the state space, the system can drive the initial state from which back to origin considering the given maximum control energy.

---

## References

[1] G.-X. Du, Q. Quan, "Degree of Controllability and its Application in Aircraft Flight Control," Journal of Systems Science and Mathematical Sciences, vol. 34, no. 12, pp. 1578-1594, 2014.
