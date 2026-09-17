---
layout: page
title: Research
permalink: /research/
description: From 3D Reconstruction to Spatial Intelligence
nav: true
nav_order: 2
---

## From 3D Reconstruction to Spatial Intelligence

My research interests have developed around one recurring question:

> **How can machines reconstruct, understand, and validate the 3D world when observations are incomplete?**

In sparse railway reconstruction, this problem appeared as missing LiDAR measurements. In monocular depth estimation, it appeared as visually plausible but metrically inaccurate geometry. In intelligent CAD, it became the difference between visual similarity and correct topology or connectivity. In autonomous driving, it further raised the question of whether improved perception actually benefits downstream behaviour.

These experiences gradually shifted my interest from 3D reconstruction toward 3D perception and spatial intelligence.

## Research Journey

### 2023 — Curiosity from Autonomous Driving

An L2 driving-assistance system first made me wonder how a machine converts sensor observations into a unified representation of lanes, vehicles, obstacles, distances, and planned trajectories.

### 2024 — Sparse 3D Reconstruction

I began working on high-speed train reconstruction from sparse LiDAR observations and encountered severe missing regions caused by glass surfaces. Instead of continuing to search for boundaries only among existing points, I explored representing missing regions explicitly through tri-axial projection and reverse hole-boundary reasoning.

**Core lesson:** Changing the representation of a problem can be more important than making the original method more complicated.

### 2025 — Learning-Based Reconstruction

I explored pretrained monocular depth models for dense railway-scene reconstruction. Although the predicted depth maps appeared visually complete, some reconstructed 3D structures exhibited incorrect relative distances.

**Core lesson:** Visual plausibility does not guarantee geometric reliability.

### 2026 — Intelligent CAD

In intelligent CAD experiments, generated models could have plausible external shapes while containing incorrect hole positions, axis locations, topology, or connections between primitives. This moved my interest from reconstructing shapes toward understanding geometry and spatial relationships.

### 2026 — Autonomous Driving

At UC Irvine, I studied KAN and physics-informed learning from PilotNet steering regression to Fast-BEV 3D detection. A key lesson came from failure: more physically reasonable auxiliary constraints did not automatically improve a more complex detection model. This strengthened my interest in hypothesis-driven experimentation and failure analysis.

### Next — Reliable Spatial Intelligence

My current interest is in combining learned priors, explicit geometry, sensor observations, and uncertainty to build more reliable 3D understanding.

## Current Questions

1. How can learned priors recover missing 3D structure without producing geometrically unsupported hallucinations?
2. How can we distinguish between visually plausible and geometrically reliable 3D predictions?
3. How can semantic priors from foundation models be combined with explicit geometry, topology, depth, and point-cloud observations?
4. When multiple 3D structures are plausible, can a model explicitly represent its uncertainty rather than producing one overconfident answer?
5. Can perception uncertainty guide active observation and downstream robotic action?

## Future Direction

My long-term interest is not simply to improve the accuracy of an isolated visual model.

I hope to study how intelligent systems can build 3D representations that are reliable, verifiable, and useful for real-world reasoning and action.

A direction I am particularly interested in is:

> Perception → Spatial Understanding → Uncertainty → Active Observation → Action

This direction may connect with robotics, autonomous systems, embodied intelligence, 3D vision, geometric intelligence, or intelligent CAD. My central research identity remains **3D Perception and Spatial Intelligence**.
