# `analytical_hierarchy_process`

## Syntax

```python
analytical_hierarchy_process(A)
analytical_hierarchy_process(A, method)
```

## Description

```python
W, CI, CR = analytical_hierarchy_process(A)
```

Compute weights of each element according to AHP and the comparison matrix `A`.

The corresponding eiginvector of the maxmum value is selected as the weights vector.

Coherence index and ratio are return as well.

---

```python
W, CI, CR = analytical_hierarchy_process(A, method)
```

The argument `method` is used to decide the way to finally get weights vector.

## Examples

```python
>>> from OpenHA.assessment.system import analytical_hierarchy_process
>>> import numpy as np
>>> A = np.array([1, 1/2, 4, 3, 3,
        2, 1, 7, 5, 5,
        1/4, 1/7, 1, 1/2, 1/3,
        1/3, 1/5, 2, 1, 1,
        1/3, 1/5, 3, 1, 1]).reshape((-5, 5))
>>> w, ci, cr = analytical_hierarchy_process(A)
>>> print(w, ci, cr)

[[0.26360349]
 [0.47583538]
 [0.0538146 ]
 [0.09806829]
 [0.10867824]] 0.018021102142554035 0.01609026977013753

```

## Input Arguments

`A` —— np.ndarray, the comparison matrix which is square.

The comparison matrix is get by pairwise comparison according to their importance to the final decision.

---

`method` —— str, optional, the way how to compute the weights vector.

The available options are `eigenvector` (default), `geometric_mean`, and `arithmetic_mean`.

- `eigenvector`: the eigenvector corresponding to the max eigenvalue.
- `geometric_mean`: the geometric mean of each row of matrix `A`.
- `arithmetic_mean`: the arithmetic mean of each row of matrix `A`.

## Output Arguments

`W` —— The weights vector.

---

`CI` —— Coherence Index

The matrix `A` is expected to be coherence.
`CI` is a index showing whether `A` is satisfied.

$$
CI = \frac{\lambda_{\max}-n}{n-1}
$$

---

`CR` —— Coherence Ratio

$$
CR = \frac{CI}{RI}
$$

where $RI$ is the corresponding Saaty random coherence.

`CR` should be less than 0.1, namely $CR<0.1$.
