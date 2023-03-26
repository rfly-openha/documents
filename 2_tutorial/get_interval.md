# `get_interval`

## Syntax

```python
get_interval(left, right)
get_interval(left, right, l_closed, r_closed)
```

## Description

```python
s = get_interval(left, right)
```

Initialize an instant of the class `MathSet`, which is an open interval.
The left and right end points are determined by `left` and `right`.

---

```python
s = get_interval(left, right, l_closed, r_closed)
```

`l_closed` and `r_closed` determine whether either side is closed. Default are `False`.

## Examples

```python
>>> from OpenHA.core.MathSet import get_interval

>>> s = get_interval(2, 5, l_closed=True, r_closed=False)
>>> print(s.has([2, 3, 4, 5]))

[True, True, True, False]
```

## Input Arguments

`left` —— float, left end point of the interval.

---

`right` —— float, right end point of the interval

---

`l_closed` —— `True` or `False`, whether the left side of the interval is closed. Default is `False`.

---

`r_closed` —— `True` or `False`, whether the right side of the interval is closed. Default is `False`.

## Properties of Arguments

| Name of the parameters | Is optional? | Source, dialog or input port? |
| :--------------------: | :----------: | :---------------------------: |
|         `left`         |      No      |            Dialog             |
|        `right`         |      No      |            Dialog             |
|       `l_closed`       |      No      |            Dialog             |
|       `r_closed`       |      No      |            Dialog             |
