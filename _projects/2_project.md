---
layout: page
title: Learning Adaptive Control Barrier Functions
description: Distilling kinodynamic expert planning into a structured, reactive safety filter.
img: assets/img/research/cbf-results.png
importance: 2
category: research
---

Control barrier function quadratic programs can enforce safety constraints at high rates, but their behavior depends on parameters that are often fixed and hand tuned. This work learns state-dependent CBF-QP parameters from a privileged kinodynamic planner. The differentiable optimization layer keeps the learned controller grounded in system dynamics and safety constraints while improving goal-directed behavior around moving obstacles.

**Paper:** *Learning Adaptive Control Barrier Functions for Safe, Real Time Motion Planning* (preprint).

![Adaptive control results](/assets/img/research/cbf-results.png)
