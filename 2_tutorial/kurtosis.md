# `kurtosis`

Compute the kurtosis.

## Syntax

```python
kurtosis(x)
```

## Description

```python
m = kurtosis(x)
```

Compute the kurtosis of all the observations.
For a random variable $X$, its kurtosis is,

$$
\text{kurtosis} = \frac{E\left[\left(X-\mu\right)^4\right]}{\sigma^4}
$$

Where $\mu = E\left(X\right)$ and $\sigma = \sqrt{D\left(X\right)}$.

And its observation is

$$
\text{kurtosis} = \sum_{i=1}^{n}\frac{\left(x_i-\bar{x}\right)^4}{n}\frac{1}{s^4}
$$

where $x_i,i=1,2,\cdots,n$ represents the $i$-th observed value, and

$$
\bar{x}=\frac{1}{n}\sum_i^n x_i,s=\sqrt{\frac{1}{n}\sum_{i=1}^{n}\left(x_i-\bar{x}\right)}
$$

## Examples

```python
>>> from OpenHA.processing.feature import kurtosis
>>> import numpy as np

# normal distribution
>>> x = np.random.randn(1000)
>>> print(kurtosis(x))

2.968569898977294

```

## Input Arguments

`x` —— A N-D array of observations.

For an n-by-m array, it indicates `n` observations with `m` features.

## Properties of Arguments

| Name of the parameters | Is optional? | Source, dialog or input port? |
| :--------------------: | :----------: | :---------------------------: |
|          `x`           |      No      |          Input port           |

## References

[1] "Measures of Skewness and Kurtosis," Online, https://www.itl.nist.gov/div898/handbook/eda/section3/eda35b.htm.
