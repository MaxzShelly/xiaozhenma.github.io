---
layout: default
title: Research
permalink: /research/
description: From 3D Reconstruction to Spatial Intelligence # Preserve the shared navigation/search entry on other pages.
display_description: Towards 3D Spatial Understanding
nav: true
nav_order: 2
---

{% capture research_body %}

## Towards 3D Spatial Understanding

**Combining Geometry, Multimodal Perception, and Large Language Models**

My research interests centre on one question: how can large models understand the physical world through 3D geometry, object structures, and spatial relationships?

I am interested in combining geometric methods with AI’s ability to interpret multi-view and multisensor observations. Geometric methods provide measurable spatial information, while learned models provide semantic knowledge, structural priors, and world knowledge. Combining the two may help models connect descriptions in images and language with explicit 3D spatial representations.

My previous projects have provided foundations for this direction at different levels, from reconstructing the geometry of individual objects to recovering scenes containing multiple objects, and then to parametric CAD structures and learning models for autonomous driving. These experiences have gradually directed my attention towards how 3D information is represented, understood, and used for reasoning.

## Research Foundations

### Object Geometry | Point Cloud Completion and Surface Reconstruction

In the high-speed train-nose reconstruction project, I carried out multisensor data acquisition and studied a point-cloud completion method combining tri-axial projection with reverse hole-boundary identification. This experience led me to examine how object geometry can be recovered from incomplete observations and how missing data affects reconstructed surfaces. It laid a foundation for my subsequent study of 3D object shapes and boundaries.

### Scene Representation | Pixel-Level 3D Reconstruction and Physical Object Extraction

In the transportation-scene reconstruction project, I explored combining multi-frame observations, monocular depth estimation, LiDAR measurements, and semantic boundary constraints, extending my work from individual shapes to scenes containing multiple physical objects. This work provided a foundation for studying object boundaries, positions, and relationships within a shared 3D coordinate system.

### Structured Geometry | Intelligent CAD

Through CAD-Assistant, ParSeNet, Point2CAD, and CAD-Recode, I studied the connections between point clouds, surface segmentation, geometric structures, and editable CAD programs. I also conducted experiments on geometric constraints, knowledge-enhanced training, and multiple-candidate generation combined with execution checks and geometric verification. These experiences strengthened my interest in how structured representations can describe an object’s composition, topology, and geometric relationships to support models in reasoning about and modifying 3D objects.

### Learning and Constraints | PIKAN-Drive

During my summer research at the University of California, Irvine, I explored KAN and physics-informed learning through PilotNet steering prediction and Fast-BEV 3D object detection, comparing the effects of prediction-head structures and additional constraints on performance. This work gave me experimental experience in combining learned models with explicit priors. It also showed me that the effectiveness of this combination needs to be verified for each specific task.

## Current Research Questions

1. How can images, point clouds, and multi-view geometry be organised into 3D representations that large models can use?
2. How can semantic recognition be connected with measurable spatial properties such as dimensions, distances, orientations, and object boundaries?
3. How can structured representations describe relationships such as connectivity, containment, adjacency, and relative position?
4. How can models select suitable geometric tools, interpret their outputs, and use them to answer spatial questions?

## Future Research Directions

I hope to explore spatial agents grounded in geometric information, connecting large models, perception systems, structured 3D representations, and geometric computation tools.

An initial direction is to enable a model to understand a spatial question, identify the relevant objects, and call appropriate tools for measurement and geometric analysis. For example, a scene agent could query object dimensions or measure the distance between two objects, while a CAD agent could inspect generated geometric structures and coordinate modelling and verification tools.

These directions will build on my existing work in 3D reconstruction and CAD, and their specific capabilities and effectiveness still need to be verified through experiments. My long-term goal is to help large models understand what objects are, how they are structured, and how they relate to one another in 3D space, and to apply this understanding to robotics, autonomous driving, and intelligent design.

{% endcapture %}

<style>
  #research-page > .post-header {
    margin-bottom: 48px;
  }
  #research-page article > h2 {
    margin: 76px 0 28px;
    line-height: 1.3;
  }
  #research-page article > h2:first-child {
    margin-top: 0;
  }
  #research-page article > h3 {
    margin: 44px 0 20px;
    line-height: 1.4;
  }
  #research-page article > h2 + h3 {
    margin-top: 0;
  }
  #research-page article > p {
    margin: 0 0 24px;
    line-height: 1.8;
  }
  #research-page article > ol {
    margin: 0 0 24px;
    padding-left: 1.5em;
    line-height: 1.8;
  }
  #research-page article li + li {
    margin-top: 16px;
  }
  @media (max-width: 575px) {
    #research-page > .post-header {
      margin-bottom: 36px;
    }
    #research-page article > h2 {
      margin-top: 56px;
      margin-bottom: 22px;
    }
    #research-page article > h3 {
      margin-top: 36px;
      margin-bottom: 18px;
    }
  }
</style>

<div class="post" id="research-page">
  <header class="post-header">
    <h1 class="post-title">{{ page.title }}</h1>
    <p class="post-description">{{ page.display_description }}</p>
  </header>
  <article>
    {{ research_body | markdownify }}
  </article>
</div>
