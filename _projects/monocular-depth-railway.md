---
layout: default
title: Monocular Depth-Driven 3D Railway Scene Reconstruction
paper_title: 稀疏点云交通场景像素级三维重建与物理对象提取
description: Combining learned depth, LiDAR anchors, and semantic boundary constraints.
importance: 2
category: Research
permalink: /projects/monocular-depth-railway/
---

<div class="post" id="railway-reconstruction-project" lang="zh-CN" markdown="1">

<header class="post-header" style="margin-bottom: 2.75rem">
  <h1 class="post-title" style="font-size: clamp(1.5rem, 2.4vw, 2rem); line-height: 1.4; margin: 0">{{ page.paper_title }}</h1>
</header>

<article style="line-height: 1.75" markdown="1">

<section aria-labelledby="railway-abstract" markdown="1">
<h2 id="railway-abstract" style="font-size: 1.5rem; margin-bottom: 1.25rem">摘要</h2>

针对交通场景中激光雷达点云采样稀疏、单目深度存在局部偏差以及遮挡区域点云归属不明确等问题，提出一种融合多帧视锥聚合、对象边界约束与校正的像素级三维重建与物理对象提取方法。以 FAST-LIVO2 输出的位姿和基础点云建立统一坐标参考，将离线采集序列中的共视点云通过视锥投影获取稠密点云，这种方法解决了传统稀疏点云难以表示完整物体边界和场景结构的问题。

进一步将单目 AI 深度估计与雷达位置约束结合，采用 SAM 3 分割结果限定局部拟合范围，以 LiDAR 测量与单目深度预测之间的残差为约束，在对象内部构建分片移动最小二乘校正模型，随后将有效像素反投影为三维点，从而实现像素级三维重建，相比纯单目生成式 SLAM 技术，该方法可保障复杂大场景下的重建精度。

使用 SAM 3 预训练模型进行多帧图像分割与边界识别，为物理对象多帧视图三维点云提取提供了技术手段。开发了分类感知的半径滤波和分片显示技术，解决多帧噪点叠加、视觉效果不佳问题，实现大场景下高精度、可视化的三维点云展示及交通资产提取。街区基础建图及铁路桥梁场景的重建结果展示了从稀疏观测到局部连续表面表达的处理过程，以及轨道和横梁等交通资产物理对象的点云提取能力。

</section>

</article>

</div>
