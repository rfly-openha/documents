# `gate_xor`

The Boolean logic gate "xor" in the fault tree.
Calculate the probability that the conditioning event happens according to the inputs.

## Syntax

```python
q = gate_xor(q1, q2)
```

## Description

```python
q = gate_xor(q1, q2)
```

Calculate the probability that the conditioning event happens according to the inputs `q1` and `q2`.

The relationship between them satisfies the following equation.

$$
q = \left(1-q_1\right)\times q_2+q_1\times\left(1-q_2\right)
$$

where $q_1,q_2\in\left[0,1\right]$.

## Examples

## Examples

```python
>>> from OpenHA.assessment.system import gate_xor
>>> q1, q2 = 0.8, 0.9
>>> print(gate_xor(q1, q2))

# (1 - 0.8) * 0.9 + 0.8 * (1 - 0.9)
# 0.2 * 0.9 + 0.8 * 0.1
# 0.18 + 0.08

0.26

```

## Input Arguments

`q1` —— The probability that an event happens, specified as a positive numeric scaler in $\left[0,1\right]$.

---

`q2` —— The probability that the other event happens, specified as a positive numeric scaler in $\left[0,1\right]$.
