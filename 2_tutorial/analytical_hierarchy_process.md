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

The Analytic Hierarchy Process is a mathematical model for decision-making problems developed by Thomas L. Saaty.

Computes the weight of each element according to pairwise comparison matrix `A`.
The eigenvector of `A` corresponding to the maximum eigenvalue is chosen as the weight vector as default.

The consistency index and ratio are returned along with the weight vector.

---

```python
W, CI, CR = analytical_hierarchy_process(A, method)
```

`method` specifies the way how to compute the weight vector.
Default is `eigenvector`.

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

`A` —— The n-by-n pairwise comparison matrix.

---

`method` —— str, optional. It specifies the way how to compute the weights vector, specified as `eigenvector` (default), `geometric_mean`, or `arithmetic_mean`.

For example, assuming a comparison matrix

$$
A=\left[\begin{matrix}a_1&a_2\\ a_3&a_4\end{matrix}\right]
$$

- `eigenvector`: The eigenvector corresponding to the maximum eigenvalue.
- `geometric_mean`: the geometric mean of each row of matrix `A`.

That is,

$$
A\Rightarrow
\left[\begin{matrix}\sqrt{a_1\cdot a_2}\\ \sqrt{a_3\cdot a_4}\end{matrix}\right]\Rightarrow\left[\begin{matrix}\frac{\sqrt{a_1\cdot a_2}}{\sqrt{a_1\cdot a_2}+\sqrt{a_3\cdot a_4}}\\ \frac{\sqrt{a_3\cdot a_4}}{\sqrt{a_1\cdot a_2}+\sqrt{a_3\cdot a_4}}\end{matrix}\right]
$$

- `arithmetic_mean`: the arithmetic mean of each row of matrix `A`.

$$
A\Rightarrow\left[\begin{matrix}\frac{a_1}{a_1+a_3}&\frac{a_2}{a_2+a_4}\\ \frac{a_3}{a_1+a_3}&\frac{a_4}{a_2+a_4}\end{matrix}\right]\Rightarrow\left[\begin{matrix}\frac{1}{2}\left(\frac{a_1}{a_1+a_3}+\frac{a_2}{a_2+a_4}\right)\\ \frac{1}{2}\left(\frac{a_3}{a_1+a_3}+\frac{a_4}{a_2+a_4}\right)\end{matrix}\right]
$$

## Properties of Arguments

| Name of the parameters | Is optional? | Source, dialog or input port? |
| :--------------------: | :----------: | :---------------------------: |
|          `A`           |      No      |            Dialog             |
|        `method`        |     Yes      |            Dialog             |

## Output Arguments

A tuple `(W, CI, CR)`, where `W` is the weight vector of length `n`, `CI` is the Consistency Index, and `CR` is the Consistency Ratio.

$$
CI = \frac{\lambda_{\max}-n}{n-1}<\frac{\sigma^2}{2}
$$

where $\frac{\sigma^2}{2}$ provides an upper bound for the measure of consistency index.

It is used as a measure of the closeness of $A$ to consistency.
So the matrix $A$ is consistency if $\lambda_{\max}=n$.

It can be noted that if $n$ is large, then $CI<\frac{\sigma^2}{2}$ even if $\lambda_{\max}$ if far away from $n$.
Therefore, for a large number of objectives, $CI$ might not provide a meaningful measure of consistency.

In order to check consistency, Satty uses both the consistency index and another measure called the random index $RI$.
A random sample of 500 pairwise reciprocal matrices is constructed.
Each matrix is generated randomly.
The average value of the consistency indexes of these 500 matrices is called
the random index $RI$.

|  n  |  1   |  2   |  3   |  4   |  5   |  6   |  6   |  8   |  9   |  10  |
| :-: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| RI  | 0.00 | 0.00 | 0.58 | 0.90 | 1.12 | 1.24 | 1.32 | 1.41 | 1.45 | 1.49 |

Since Saaty suggests using the AHP
when the number of objectives is less than 10, this table only lists the $RI$ for
matrices up to order 10.

The consistency ratio of a matrix is the ratio of $CI$ the of that matrix
to the $RI$ for the same matrix order.
That is,

$$
CR = \frac{CI}{RI}
$$

If the consistency ratio is 0.10 or less, the decision-maker is not too
inconsistent and the result obtained by the AHP is acceptable.

## References

[1] G. H. Nguyen, "The Analytic Hierarchy Process: A Mathematical Model for Decision Making Problems" (2014). Senior Independent Study Theses. Paper 6054. https://openworks.wooster.edu/independentstudy/6054
