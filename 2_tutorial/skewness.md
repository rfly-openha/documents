# `skewness`

Compute the skewness.

## Syntax

```python
skewness(x)
```

## Description

```python
m = skewness(x)
```

Compute the skewness of all the observations.
For a random variable $X$, its skewness is,

$$
\text{skewness} = \frac{E\left[\left(X-\mu\right)^3\right]}{\sigma^3}
$$

Where $\mu = E\left(X\right)$ and $\sigma = \sqrt{D\left(X\right)}$.

And its observation is

$$
\text{skewness} = \sum_{i=1}^{n}\frac{\left(x_i-\bar{x}\right)^3}{n}\frac{1}{s^3}
$$

where $x_i,i=1,2,\cdots,n$ represents the $i$-th observed value, and

$$
\bar{x}=\frac{1}{n}\sum_i^n x_i,s=\sqrt{\frac{1}{n}\sum_{i=1}^{n}\left(x_i-\bar{x}\right)}
$$

## Examples

```python
>>> from OpenHA.processing.feature import skewness
>>> import numpy as np

# sample from a normal distribution
>>> x = np.random.randn(1000)
>>> print(skewness(x))

0.032533505273764085

```

## Input Arguments

`x` —— A N-D array of observations.

For an n-by-m array, it indicates `n` observations with `m` features.

## References

[1] "Measures of Skewness and Kurtosis," Online, https://www.itl.nist.gov/div898/handbook/eda/section3/eda35b.htm.
