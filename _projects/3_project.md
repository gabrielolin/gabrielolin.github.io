---
layout: page
title: MPPI for Whole-Body Wheeled Locomotion
description: Sampling-based predictive control with wheel rolling constraints in simulation.
img: assets/gif/quadruped_terrain.gif
importance: 3
category: research
---

This project adapts Model Predictive Path Integral (MPPI) control to wheeled quadruped locomotion in MuJoCo. It explores how to account for wheel rolling constraints while planning whole-body motions across walking, waypoint navigation, stairs, and rough terrain.

At each control step, MPPI samples `N` control sequences from a time-varying Gaussian around the current nominal sequence. Each sequence is simulated over a horizon and scored using tracking, control-effort, and constraint costs. Lower-cost rollouts receive exponentially larger weights; their weighted average updates the nominal controls, which are then smoothed with cubic splines.

$$
\begin{aligned}
\text{Sample controls:}\qquad
&u_t^{(k)} \sim \mathcal{N}(\mu_t,\Sigma_t), \\
&\tilde{u}_t^{(k)} = u_t + \epsilon_t^{(k)}, \quad t=0,\ldots,H-1.
\end{aligned}
$$

The rollout cost combines state-tracking error, control effort, and smoothness:

$$
J^{(k)} = \sum_{t=0}^{H-1}\left[
  (\Delta x_t^{(k)})^\top Q\Delta x_t^{(k)}
  + (\Delta u_t^{(k)})^\top R\Delta u_t^{(k)}
  + \|\Delta p_t^{(k)}\|_1
\right].
$$

Normalize the rollout costs into importance weights, then update the sequence with their weighted controls:

$$
\begin{aligned}
w_k &= \frac{\exp\!\left(-\frac{J^{(k)}-J_{\min}}{\lambda}\right)}
{\sum_{j=1}^{N}\exp\!\left(-\frac{J^{(j)}-J_{\min}}{\lambda}\right)},\\[4pt]
\mu_t &\leftarrow \sum_{k=1}^{N} w_k\,\tilde{u}_t^{(k)}.
\end{aligned}
$$

![MPPI rollout and weighted control update diagram](/assets/img/mppi_diagram.png)

Execute the first updated control, shift the sequence forward, and repeat. For wheeled locomotion, the dynamics and costs account for wheel rolling constraints, slip, and the nonholonomic no-sideways-motion condition; wheel torques can also be optimized directly.

![Wheeled quadruped traversing rough terrain in simulation](/assets/gif/quadruped_terrain.gif)
