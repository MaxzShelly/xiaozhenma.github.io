---
layout: page
title: Intelligent CAD and Geometric Understanding
description: From visual similarity to geometry, topology, and parametric validity.
importance: 3
category: Research
permalink: /projects/intelligent-cad/
---

<!-- TODO: add CAD generation and point-cloud geometry result images -->

## Core Question

> **If a generated 3D object looks correct, is it actually geometrically correct?**

At the Institute of Automation, Chinese Academy of Sciences, I explored intelligent CAD generation and point-cloud geometric understanding.

## Intelligent CAD Generation

In tests of a pretrained CAD generation model, external shape could look plausible while hole positions, axis locations, primitive connections, topology, or parametric validity were incorrect. I worked on prompt optimisation and incorporating dimensional and geometric constraints.

> Visual similarity ≠ geometric correctness

Appearance → Geometry → Topology → Parametric validity

## Point-Cloud Geometric Understanding

This was a separate sub-direction from CAD prompt optimisation. I reproduced Point2CAD and ParSeNet, explored multi-view projection boundary information, and investigated geometric consistency.

## Future Idea

Generation → Geometric validation → Error localisation → Local correction → Re-execution
