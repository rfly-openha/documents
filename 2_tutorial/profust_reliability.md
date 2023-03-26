# `profust_reliability`

Compute the profust reliability according to the research in [1].

## Syntax

```python
profust_reliability(s, msf)
```

## Description

```python
R = profust_reliability(s, msf)
```

Compute the profust reliability according to the research in [1].

`s` is an array of system state vectors if `msf` is not `None`.
Otherwise, `s` is an array of the degree of membership of system states, and the `msf` specifies the membership function.

Suppose that the system is in a specific state $S_q$ at time $t_0$ for certain, and the system is in a specific state $S_j$ at time $t$ for certain.

Then the profust reliability is

$$
R\left(t\right)=\mu_S\left(S_q\right)\left[1-\mu_{T_{\text{SF}}}\left(m_{qj}\right)\right]
$$

More details and the proof are available in [1].

## Examples

```python
>>> from OpenHA.assessment.attribute import profust_reliability, trapezoidal_membership_func
>>> import numpy as np
>>> import pandas as pd
# TODO: the way to load dataset
>>> x = pd.read_csv(r'E:\OpenHA_\test\examples\data_zzy.csv', header=None)
# select the data of the last column
# the height of a multicopter
>>> x = x[3]
# parameters for the trapezoidal membership function
>>> a = 9.8
>>> c = 9.95
>>> d = 10.05
>>> b = 10.2
# construct the membership function
>>> f = lambda x: trapezoidal_membership_func((a, b, c, d), x)
# call the function
>>> y = profust_reliability(x, f)

```

## Input Arguments

`s` —— An array of system state vectors if `msf` is not None.
Otherwise, its an array of the degree of membership of system states.

---

`f` —— The membership function, specified as a callble object, or just `None`.

The membership function represents the degree of membership between an element and a set.
In fuzzy mathematics, the degree of membership is in $[0,1]$.

## Properties of Arguments

| Name of the parameters | Is optional? | Source, dialog or input port? |
| :--------------------: | :----------: | :---------------------------: |
|          `s`           |      No      |          Input port           |
|          `f`           |      No      |            Dialog             |

## References

[1] Z. Zhao, Q. Quan, K.-Y. Cai, "A modified profust-performance-reliability algorithm and its application to dynamic systems," Journal of Intelligent & Fuzzy Systems, vol. 32, no. 1, pp. 643-660, 2017. DOI: 10.3233/JIFS-152544.
