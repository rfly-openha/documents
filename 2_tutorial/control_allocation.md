# `control_allocation`

Returns the control allocation matrix of a multicopter.

## Syntax

```python
control_allocation(n, d, ku)
control_allocation(n, d, ku, **kwargs)
```

## Description

```python
B_f = control_allocation(n, d, ku)
```

Returns the control allocation matrix of a multicopter with `n` propellers.
The parameter `d` specifies the distance from each propeller to the origin of the body coordinate.
And `ku` specifies the ratio of the torque to thrust of each propeller.

---

```python
B_f = control_allocation(n, d, ku, **kwargs)
```

More parameters of the propulsion system of a multicopter are specified by `kwargs`.
See [Input Arguments](#input-arguments) for more information.

## Examples

1. Assuming there is a Plus-shape quadcopter, the distance between each propeller and the origin of body coordinate are the same, that is `d = 0.28`. And `ku = 0.1`.

```python
>>> from OpenHA.assessment.attribute import control_allocation

>>> control_allocation(4, 0.28, 0.1)

array([[ 1.00000000e+00,  1.00000000e+00,  1.00000000e+00,
         1.00000000e+00],
       [ 0.00000000e+00, -2.80000000e-01, -3.42901104e-17,
         2.80000000e-01],
       [ 2.80000000e-01,  1.71450552e-17, -2.80000000e-01,
        -5.14351656e-17],
       [-1.00000000e-01,  1.00000000e-01, -1.00000000e-01,
         1.00000000e-01]])
```

---

2. Assuming an X-shape quadcopter that is equipped with almost the same propulsion system with the above one, and its yaw angle is uncontrollable yet.

```python
>>> from OpenHA.assessment.attribute import control_allocation

>>> control_allocation(4, 0.28, 0.1, init_angle=math.pi / 4, giveup_yaw=True)

array([[ 1.       ,  1.       ,  1.       ,  1.       ],
       [-0.1979899, -0.1979899,  0.1979899,  0.1979899],
       [ 0.1979899, -0.1979899, -0.1979899,  0.1979899]])
```

## Input Arguments

`n` —— The number of propellers of a multicopter. Specified as a positive integer scalar.

---

`d` —— The distance between each propeller and the origin of the body coordinate.

When all distances are almost equal, specify `d` as a positive value.
For example, `d = 0.28`.

Otherwise, specify `d` as an array of positive values of length `n`.
For example, `d = [0.28 0.35 0.28 0.35]`.

---

`ku` —— The ratio of the torque to thrust of each propeller.

When all ratios are almost equal, specify `ku` as a positive value.
For example, `ku = 0.1`.

Otherwise, specify `ku` as an array of positive values of length `n`.

---

`init_angle` —— The angle from $O_\text{b}x_\text{b}$ axis to each supporting arm of the propeller in clockwise direction in radians. Specified as `0` (default), real numeric scalar, or an array of positive values of length `n`.

When all the propellers are distributed evenly, specify `init_angle` as a positive value.
It then indicates the angle of propeller #1, namely $\phi_1$ = `init_angle`.
So, there are

$$
\phi_i=\phi_1+\frac{2\pi}{n}\left(i-1\right),i=1,2,\cdots,n.
$$

Otherwise, specify `init_angle` as an array of numeric values of length `n`.
That is, $\phi_i,i=1,2,\cdots,n$ are assigned seperately.

---

`drct` —— The rotation direction of each propeller. Specified as an array of length `n`, in which each element is `-1` or `1`. Default is `[1, -1, 1, -1, 1, -1]`.

- `1` means the corresponding propeller rotates counterclockwise.
- `-1` means the corresponding propeller rotates clockwise.

---

`eta` —— The efficient coefficient of each propeller. Specified as `1` (default), a numeric value in $\left[0,1\right]$, or an array of length `n`, in which each element is in $\left[0,1\right]$.

---

`giveup_height` —— Whether to give up the control of height or not. `True` or `False` (default).

The height control of the aircraft will be given up if it's `True`.
Correspondingly, the first row of the original 4-by-n matrix will be removed.

---

`giveup_yaw` —— Whether to give up the control of yaw or not. `True` or `False` (default).

The yaw control of the aircraft will be given up if it's `True`.
Correspondingly, the fourth row of the original 4-by-n matrix will be removed.

## References

[1] Q. Quan. Introduction to Multicopter Design and Control. Singapore: Springer, 2017.
