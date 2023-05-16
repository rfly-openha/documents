# Mathematical Model of the Multicopter

## Introduction

The multicopter are quite commonly-seen in our daily life nowadays.
Due to their advantages, such as flexibility, low cost, and easy to operate, multicopters now are widely used in military and civilian fields.
In this article, the nonlinear mathematical model of the most common multicopters will be given.
The physical parameters of simulation model that we adopted in the software-in-the-loop (SIL) and hardware-in-the-loop (HIL) will also be introduced in the end.

## Modeling

The multicopter is usually equipped with $n_{P}$ propellers.
The mapping from the thrust $f_{i},i=1,\cdots,{n_{P}}$ of each propeller to the thrust and torque vector $\mathbf{u}_{f}\triangleq\left[\begin{matrix}u_t & \tau_x & \tau_y & \tau_z\end{matrix}\right]^{\text{T}}$ is given by $\mathbf{u}_f=\mathbf{B}_f\mathbf{f}$, where $\mathbf{f}\triangleq\left[\begin{matrix}f_1 & f_2 & \cdots & f_{n_{P}}\end{matrix}\right]^{\text{T}}$, and $\mathbf{B}_f\in\mathbb{R}^{4\times n_P}$ is the control allocation matrix.
$\mathbf{B}_f$ is specified as

$$
\mathbf{B}_{f}=\left[\begin{matrix}
1                                & \cdots & 1                                                      \\
-r_{1}\sin\varphi_1 & \cdots & -r_{n_P}\sin\varphi_{n_\text{p}} \\
r_{1}\cos\varphi_1  & \cdots & r_{n_P}\cos\varphi_{n_\text{p}}  \\
w_{1}k_{\mu,1}      & \cdots & w_{n_P}k_{\mu,n_P}
\end{matrix}\right]
$$

where $r_{i},i=1,\cdots,n_P$ is the distance from the center of the $i$-th propeller to the center of mass, $k_{\mu,i},i=1,\cdots,n_P$ is the ratio of thrust to torque of the $i$-th propeller and $w_{i},i=1,\cdots,n_P$ is defined by

$$
w_i=\begin{cases}
1,&\text{if rotor \# i rotates anticlockwise}\\
-1,&\text{if rotor \# i rotates clockwise}\\
\end{cases}
$$

and $\varphi_{i},i=1,\cdots,n_P$ are shown in the following figure.

<img src="./Fig_1.png" style="zoom: 33%;" />

Let $\mathcal{I}=\left\{\mathbf{e}_{x},\mathbf{e}_{y},\mathbf{e}_{z}\right\}$ denote a right-hand inertial frame and $\mathcal{A}=\left\{\mathbf{e}_{1},\mathbf{e}_{2},\mathbf{e}_{3}\right\}$ denote a (right-hand) body fixed frame rigidly attached to the aircraft where the center of gravity (CoG) of the multicopter is chosen as the origin of $\mathcal{A}$.

Then, the rigid body equations of motion of a multicopter are given by

$$
\left\{\begin{aligned}
\dot{\mathbf{p}}_\text{e}& =\mathbf{v}_\text{e}\\
\dot{\mathbf{v}}_\text{e}& =\mathbf{g}+\mathbf{R}_\text{be}\frac{\mathbf{F}}{m_a}\\
\dot{\mathbf{\Theta}}& =\mathbf{W}\boldsymbol{\omega}\\
\mathbf{J}\dot{\boldsymbol{\omega}} & =-\boldsymbol{\omega}\times\left(\mathbf{J}\cdot\boldsymbol{\omega}\right)+\mathbf{G}_a+\boldsymbol{\tau}
\end{aligned}\right.
$$

where $m_a$ denotes the mass of the multicopter, $g$ denotes the gravitational acceleration,
$\mathbf{e}_{3}\triangleq\left[\begin{matrix} 0 & 0 & 1 \end{matrix}\right]^{\text{T}}$ denotes the unit vector in $\mathcal{A}$, and $\mathbf{G}_{a}$ represents the gyroscopic torques.

The vectors $\mathbf{p}\triangleq\left[\begin{matrix} x & y & h \end{matrix}\right]^{\text{T}}$ and $\mathbf{v}\triangleq\left[\begin{matrix} v_x & v_y & v_h \end{matrix}\right]^{\text{T}}$ denote the position and linear velocity of the origin of $\mathcal{A}$ with respect to $\mathcal{I}$.
The matrix $\mathbf{J}\triangleq\text{diag}\left(J_x,J_y,J_z\right)\in\mathbb{R}^{3\times3}$ is the constant inertia matrix.
The matrix $\mathbf{R}_\text{be}$ represents the rotation matrix rotating vectors from frame $\mathcal{A}$ to frame $\mathcal{I}$, and the matrix $\mathbf{W}$ represents the relationship between the attitude rate and the aircraft body's angular velocity.

$$
\mathbf{W}=\left[\begin{matrix}
1 & \tan\theta\sin\phi  & \tan\theta\cos\phi  \\
0 & \cos\phi            & -\sin\phi           \\
0 & \sin\phi/\cos\theta & \cos\phi/\cos\theta
\end{matrix}\right]
$$

As shown in the following figure, the propulsor model that we adopt includes not only a DC motor but also an ESC and a propeller.
Throttle command $\sigma\in\left[0,1\right]$ is an input signal between 0 and 1, while the battery output
voltage $U_\text{b}$ cannot be controlled.

<img src="./propulsion.svg" style="zoom: 100%;" />

The ESC generates an equivalent average voltage $U_\text{m} = \sigma U_\text{b}$ after receiving the throttle command $\sigma$ and the battery output voltage $U_\text{b}$.
First, given a voltage signal, the motor can achieve a steady-state speed $\varpi_\text{ss}$.
The relation is normally linear, which is expressed as

$$
\varpi_{ss}=C_\text{b}U_\text{b}\sigma+\varpi_\text{b}
$$

$\varpi_\text{b}$ are constant parameters.
Secondly, when given a throttle command, the motor needs some time to achieve the steady-state speed $\varpi_{ss}$.
This time constant denoted by $T_\text{m}$ will determine the dynamic response.
Generally, dynamics of a brushless DC motor can be simplified as a first-order low-pass filter.
Its transfer function is expressed as

$$
\frac{\varpi}{\varpi_{ss}}=\frac{k_\text{m}}{T_\text{m}s+1}
$$

In others words, when given a desired steady-state speed $\varpi_{ss}$, the motor speed cannot achieve $\varpi_{ss}$ immediately.
This process needs some time to adjust.
Combining the above two equations, one has a complete propulsor model as follows:

$$
\varpi=\frac{C_\text{b}U_\text{b}\sigma+\varpi_\text{b}}{T_\text{m}s+1}
$$

where the input is the throttle command $\sigma$ and the output is motor speed $\varpi$.

The propeller thrust and torque is expressed as

$$
\left\{\begin{aligned}
    f_i & =k_{c_\text{T},i}c_{\text{T},i}\varpi_i^2 \\
    M_i & =k_{\mu,i}\cdot f_i
\end{aligned}\right.
$$

where $c_\text{T},k_{\mu}$ is modeled as a constant that can be easily determined by experiments.
\where Mi is the reaction torque of the ith propeller acting on the fuselage, cM =1/4π 2 · ρDp5CM
can also be determined by experiments. The parameters ρ, Dp, CT, CM are presented in Sect. 4.2.1 in

## Parameters

The values of all the parameters that mentioned above are listed in the following table.

| Parameters        | Values                   | Unit                                            |
| ----------------- | ------------------------ | ----------------------------------------------- |
| $n_P$             | $4$                      |                                                 |
| $m_a$             | $1.4$                    | $\text{kg}$                                     |
| $g$               | $9.8$                    | $\text{m}/\text{s}^2$                           |
| $J_x,J_y,J_z$     | $0.0211, 0.0219, 0.0366$ | $\text{kg}\cdot\text{m}^2$                      |
| $C_\text{b}$      | $1148/12.6$              | $\text{rad}/\left(\text{s}\cdot\text{V}\right)$ |
| $U_\text{b}$      | $12.6$                   | $\text{V}$                                      |
| $\omega_\text{b}$ | $-141.4$                 | $\text{rad}/\text{s}$                           |
| $c_T$             | $0.0161$                 | $\text{N}\cdot\text{s}^2$                       |
| $k_{\mu}$         | $1.105\times 10^{5}$     | $\text{m}^{-1}$                                 |
