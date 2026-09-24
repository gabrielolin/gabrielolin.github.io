---
layout: page
title: Improving Diffusion Policies with Latent Noise Steering
description: Reinforcement learning adapts a pretrained diffusion policy for planar pushing.
img: assets/gif/pusht.gif
importance: 4
category: research
---

This project studies planar, non-prehensile manipulation: pushing and reorienting a T-shaped object with a robot arm. A pretrained diffusion policy generates action sequences from observation and sampled latent noise. Instead of retraining that policy, a learned steering policy selects the initial noise to improve task performance.

In the original policy, initial noise is sampled from a fixed Gaussian. A learned latent-noise actor `πᵂφ` instead chooses that noise, which the frozen diffusion policy maps to an action sequence: `w ~ πᵂφ(· | s)`, `a = πdp(s, w)`. Only the steering actor and critics are learned; the diffusion policy remains fixed. This follows the latent-action actor–critic formulation in [Wagenmaker et al. (CoRL 2025)](https://proceedings.mlr.press/v305/wagenmaker25a.html).

The method uses an action-space critic `Qᴬ` and a latent-noise critic `Qᵂ`. The action critic learns from environment transitions `(s, a, r, s′)`:

$$
\mathcal{L}_{Q^{\mathcal{A}}} =
\mathbb{E}\!\left[
\left(Q^{\mathcal{A}}(s,a) - r - \gamma \bar{Q}^{\mathcal{A}}(s',a')\right)^2
\right],
\qquad a' \sim \pi_{\mathrm{dp}}(s').
$$

The latent critic distills action values through the frozen diffusion policy, and the actor chooses noise with high predicted value:

$$
\mathcal{L}_{Q^{\mathcal{W}}} =
\mathbb{E}_{s,\,w\sim\mathcal{N}(0,I)}\!\left[
\left(Q^{\mathcal{W}}(s,w) - Q^{\mathcal{A}}(s,\pi_{\mathrm{dp}}(s,w))\right)^2
\right],
\qquad
\max_{\phi}\;\mathbb{E}_{s,\,w\sim\pi^{\mathcal{W}}_{\phi}(\cdot\mid s)}
\left[Q^{\mathcal{W}}(s,w)\right].
$$

The Push-T demonstrations were collected by joystick teleoperation, with fixed-pose and randomized start/goal datasets. The presentation also describes validating the diffusion policy on a long-horizon point-maze task. The reported limitation is weaker recovery from out-of-distribution states and start/goal configurations.

![Latent noise candidates are mapped by the diffusion policy to robot actions.](/assets/img/dsrl.png)

![A robot arm pushing a T-shaped object in the Push-T simulation.](/assets/gif/pusht.gif)

<a href="/assets/pdf/Improving%20Diffusion%20Policies%20with%20Latent%20Noise%20Steering%20for%20Planar%20Manipulation%20.pdf">Project presentation (PDF)</a> · Gabriel Olin and Benji Li
