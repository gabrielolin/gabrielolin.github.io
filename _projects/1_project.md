---
layout: page
title: Think Fast — Real-Time Belief-Space Planning for Projectile Interception
description: A kinodynamic action tree for fast, uncertainty-aware interception on a real robot arm.
img: assets/img/research/projectile-planning.png
importance: 1
category: research
---

Intercepting a fast-moving object means planning while its trajectory is still uncertain. This work combines adaptive Kalman-filter tracking with an offline action tree of dynamically feasible motion primitives. Online belief updates quickly re-evaluate reachability across candidate intercept locations, allowing a six degree-of-freedom ABB IRB-1600 arm to move while observations continue to arrive.

**Paper:** *Think Fast: Real-Time Kinodynamic Belief-Space Planning for Projectile Interception* (ICRA 2026).

![Robot interception setup](/assets/img/research/robot-shield.png)

![Interception planning results](/assets/img/research/interception-results.png)

<video controls playsinline preload="metadata" style="width: 100%; border-radius: 0.5rem;">
  <source src="/assets/video/projectile-interception.mp4" type="video/mp4">
  Your browser does not support embedded video.
</video>
