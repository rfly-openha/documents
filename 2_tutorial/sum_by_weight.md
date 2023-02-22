# `sum_by_weight`

## Syntax

```python
sum_by_weight(weights, elements)
```

## Description

```python
sum = sum_by_weight(weights, elements)
```

Compute weighted sum. `weights` and `elements` both are arraies of length `n`.

This method returns the weighted sum, namely

$$
\sum_{i=1}^{n}w_ix_i
$$

where $w_i$ is the weight of the i-th elements $x_i$, and $i=1,2,\cdots,n$.

## Examples

```python
>>> from OpenHA.assessment.system import sum_by_weight
>>> import numpy as np

>>> weight = np.array([0.1, 0.2, 0.3, 0.4])
>>> elements = np.random.random((4,))
>>> sum_by_weight(weight, elements)

0.31787561946429277

```

## Input Arguments

`weights` —— Array of weights of each element.

The length of `weights` should be equal to that of `elements`.

And the following equation should be satisfied.

$$
\sum_{i=1}^nw_i=1,w_i>0
$$

---

`elements` —— Array of all the elements, whose length is equal to that of `weights`.
