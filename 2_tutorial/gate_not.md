# `gate_not`

The Boolean logic gate "not" in the fault tree.
Calculate the probability that the conditioning event happens according to the inputs.

## Syntax

```python
q = gate_not(q1, q2)
```

## Description

```python
q = gate_not(q1, q2)
```

Calculate the probability that the conditioning event happens according to the input `q1`.

The relationship between them satisfies the following equation.

$$
q = 1-q_1
$$

where $q_1\in\left[0,1\right]$.

## Examples

## Examples

```python
>>> from OpenHA.assessment.system import gate_not
>>> q1 = 0.2
>>> print(gate_not(q1))

0.2

```

## Input Arguments

`q1` —— The probability that an event happens, specified as a positive numeric scaler in $\left[0,1\right]$.
