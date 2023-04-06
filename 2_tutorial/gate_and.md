# `gate_and`

The Boolean logic gate "and" in the fault tree.
Calculate the probability that the conditioning event happens according to the inputs.

## Syntax

```python
q = gate_and(q1, q2)
```

## Description

```python
q = gate_and(q1, q2)
```

Calculate the probability that the conditioning event happens according to the inputs `q1` and `q2`.

The relationship between them satisfies the following equation.

$$
q = q_1\times q_2
$$

where $q_1,q_2\in\left[0,1\right]$.

## Examples

## Examples

```python
>>> from OpenHA.assessment.system import gate_and
>>> q1, q2 = 0.8, 0.9
>>> print(gate_and(q1, q2))

0.72

```

## Input Arguments

`q1` —— The probability that an event happens, specified as a positive numeric scaler in $\left[0,1\right]$.

---

`q2` —— The probability that the other event happens, specified as a positive numeric scaler in $\left[0,1\right]$.
