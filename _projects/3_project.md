---
layout: page
title: Whole-Body Motion Planning for Wheeled Quadrupeds
description: Sampling-based predictive control with wheel rolling constraints in simulation.
importance: 3
category: research
---

This project adapts Model Predictive Path Integral (MPPI) control to wheeled quadruped locomotion in MuJoCo. It explores how to account for wheel rolling constraints while planning whole-body motions across walking, waypoint navigation, stairs, and rough terrain.

At each control step, sample `N` candidate control sequences around the nominal sequence `μ`, simulate each for horizon `T`, and compute its cost `Jₙ`. Convert costs to normalized weights and update the nominal controls:

$$
w_n = \frac{\exp(-(J_n-J_{\min})/\lambda)}{\sum_j \exp(-(J_j-J_{\min})/\lambda)},\qquad
\mu_t \leftarrow \sum_n w_n u_{n,t}.
$$

Execute the first updated control, shift the sequence forward, and repeat. To model wheeled motion, constrain the dynamics or project sampled controls onto feasible rolling motion; penalize slip and violations of the nonholonomic no-sideways-motion condition. The project also explores optimizing wheel torques directly.

<div style="border: 1px dashed #8993a4; border-radius: 0.5rem; padding: 2rem; margin: 1rem 0; text-align: center;"><strong>Figure placeholder</strong><br>Wheeled quadruped and MPPI planning overview</div>

<div style="border: 1px dashed #8993a4; border-radius: 0.5rem; padding: 2rem; margin: 1rem 0; text-align: center;"><strong>GIF / video placeholder</strong><br>Stairs, box jump, or rough-terrain simulation</div>

<a href="/assets/pdf/OCRL25_Liu_Li_Olin_Kou.pdf">Project presentation (PDF)</a> · Wensen Liu, Benji Li, Gabriel Olin, and Henry Kou · March 2025
