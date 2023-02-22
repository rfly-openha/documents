# `split_dataset`

Split dataset randomly.

## Syntax

```python
split_dataset(X, Y)
split_dataset(X, Y, percent)
```

## Description

```python
X1, Y1, X2, Y2 = split_dataset(X, Y)
```

Split the dataset with samples `X` and labels `Y` randomly into `X1, X2, Y1, Y2`.
The order of the samples remain unchanged.
The ratio of the numbers of samples in `X1` and that of `X` is 15% as default.

---

```python
X1, Y1, X2, Y2 = split_dataset(X, Y, percent)
```

The ratio of the numbers of samples in X1 and that of X is determined by `percent`.

## Examples

## Input Arguments

`X` —— List of samples of length `n`.

---

`Y` —— List of samples of length `n`.

---

`percent` —— The ratio of the numbers of samples in `X1` and that of `X`.

## Output Arguments

`X1` —— The samples that are selected our `X`, and its length is `round(percent * n)`

---

`Y1` —— The corresponding labels that selected out of `Y`, and its length is equal to that of `X1`

---

`X2` —— All the samples that not belong to `X1`.

---

`Y2` —— All the samples that not belong to `Y1`.
