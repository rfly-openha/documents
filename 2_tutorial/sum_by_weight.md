# `sum_by_weight`

## Syntax

```python
sum_by_weight(weights, elements)
```

## Description

```python
sum = sum_by_weight(weights, elements)
```

Calculates the weighted sum.
`weights` specifies the weight vector, and `elements` is an array of the values of all the elements.

The weighted sum is

$$
s  = \sum_{i=1}^{n}w_ix_i
$$

where $w_i$ is the weight of the $i$-th value $x_i$, and $i=1,2,\cdots,n$.

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

`weights` —— The weight vector, specified as an array of positive numeric scalar of length `n`.

And it should satisfy

$$
\sum_{i=1}^nw_i=1,w_i>0
$$

---

`elements` —— Array of values of all the elements, specified as an array of length `n`.



## Properties of Arguments

| Name of the parameters | Is optional? | Source, dialog or input port? |
| :--------------------: | :----------: | :---------------------------: |
|       `weights`        |      No      |          Input port           |
|       `elements`       |      No      |          Input port           |
