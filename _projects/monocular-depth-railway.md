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

<section aria-labelledby="railway-overview" style="margin-top: 3.5rem" markdown="1">
<h2 id="railway-overview" style="font-size: 1.5rem; margin-bottom: 1.25rem">Overview</h2>

本研究关注如何在统一度量坐标系下，利用 LiDAR 真实测量约束图像深度估计，同时限制跨物理对象的传播。流程以物理对象为局部处理单元：首先通过关键帧视锥选择多帧共视观测，为同一图像区域建立几何支撑；随后利用对象分割限定残差拟合范围，由 LiDAR 锚点校正对象内部的单目深度；最后结合候选点一致性筛选、距离分段分类滤波和点云组织，形成可浏览、可提取的三维场景。

流程采用离线处理设置，共视集合可包含关键帧前后的观测，主要面向静态交通基础设施。度量测量、表面先验与对象边界相互约束，共同支持从稀疏观测到有效对象区域内像素级三维采样的转换。

<figure id="railway-figure-1" style="margin: 1.75rem 0 0">
<div style="min-width: 0">
    <a href="{{ '/assets/img/railway-reconstruction/results/pipeline.png' | relative_url }}" target="_blank" rel="noopener" aria-label="查看原图：多帧视锥聚合、对象约束深度校正与像素级三维输出的整体流程，以及对象边界、包络一致性、分片残差拟合和反投影步骤">
      <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/railway-reconstruction/results/pipeline.png' | relative_url }}" width="1442" height="642" loading="lazy" alt="多帧视锥聚合、对象约束深度校正与像素级三维输出的整体流程，以及对象边界、包络一致性、分片残差拟合和反投影步骤">
    </a>
  </div>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 1.</strong> 整体重建流程与对象约束深度校正。实测 LiDAR 点为局部深度提供几何支撑，对象边界限定校正与反投影范围。点击任意图片可查看原图。</figcaption>
</figure>

<h3 style="font-size: 1.25rem; margin-top: 2rem; margin-bottom: 1rem">Main Contributions</h3>

- **多帧几何关联：**建立共视点云与关键帧像素之间的对应关系，将视锥内的真实观测组织为对象级深度校正的候选支撑。
- **对象约束深度校正：**结合对象边界与分片移动最小二乘残差拟合，在有效区域内实现由稀疏度量锚点到像素级三维采样的转换。
- **场景组织与资产提取：**围绕跨帧对象归属与大场景管理，组织深度一致性筛选、距离分段分类滤波和交通资产提取，并通过真实场景展示其作用与适用边界。

</section>

<section aria-labelledby="railway-results" style="margin-top: 3.5rem" markdown="1">
<h2 id="railway-results" style="font-size: 1.5rem; margin-bottom: 1.75rem">Results</h2>

<section aria-labelledby="railway-mapping" markdown="1">
<h3 id="railway-mapping" style="font-size: 1.25rem; margin-bottom: 1rem">基础场景重建与多帧聚合</h3>

街区与铁路桥梁的基础点云呈现了建筑立面、道路周边结构、桥梁立柱、横梁及轨道的空间布局。通过关键帧视锥聚合多帧观测，并结合对象边界筛选，提取出桥梁主体点云，为后续对象内部的深度校正与表面重建提供测量支撑。

<figure id="railway-figure-2" style="margin: 1.75rem 0 0">
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 20rem), 1fr)); gap: 1.5rem; align-items: start">
<div style="min-width: 0">
    <a href="{{ '/assets/img/railway-reconstruction/results/urban-map.png' | relative_url }}" target="_blank" rel="noopener" aria-label="查看原图：FAST-LIVO2 建立的街区基础点云">
      <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/railway-reconstruction/results/urban-map.png' | relative_url }}" width="997" height="568" loading="lazy" alt="FAST-LIVO2 建立的街区基础点云">
    </a>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">（a）街区场景</p>
  </div>
<div style="min-width: 0">
    <a href="{{ '/assets/img/railway-reconstruction/results/railway-map.png' | relative_url }}" target="_blank" rel="noopener" aria-label="查看原图：FAST-LIVO2 建立的铁路桥梁基础点云">
      <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/railway-reconstruction/results/railway-map.png' | relative_url }}" width="997" height="558" loading="lazy" alt="FAST-LIVO2 建立的铁路桥梁基础点云">
    </a>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">（b）铁路桥梁场景</p>
  </div>
  </div>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 2.</strong> FAST-LIVO2 建立的街区与铁路桥梁基础点云。</figcaption>
</figure>

<figure id="railway-figure-3" style="margin: 1.75rem 0 0">
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 20rem), 1fr)); gap: 1.5rem; align-items: start">
<div style="min-width: 0">
    <a href="{{ '/assets/img/railway-reconstruction/results/single-frame.png' | relative_url }}" target="_blank" rel="noopener" aria-label="查看原图：单帧采样得到的稀疏铁路桥梁点云">
      <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/railway-reconstruction/results/single-frame.png' | relative_url }}" width="588" height="320" loading="lazy" alt="单帧采样得到的稀疏铁路桥梁点云">
    </a>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">（a）单帧稀疏采样</p>
  </div>
<div style="min-width: 0">
    <a href="{{ '/assets/img/railway-reconstruction/results/object-candidates.png' | relative_url }}" target="_blank" rel="noopener" aria-label="查看原图：多帧聚合后经关键帧视锥与识别区域筛选的桥梁候选点云">
      <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/railway-reconstruction/results/object-candidates.png' | relative_url }}" width="478" height="309" loading="lazy" alt="多帧聚合后经关键帧视锥与识别区域筛选的桥梁候选点云">
    </a>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">（b）视锥与对象边界内的候选点云</p>
  </div>
  </div>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 3.</strong> 单帧稀疏点云与多帧聚合、对象边界筛选后的桥梁点云。</figcaption>
</figure>

</section>

<section aria-labelledby="railway-fusion" style="margin-top: 3.5rem" markdown="1">
<h3 id="railway-fusion" style="font-size: 1.25rem; margin-bottom: 1rem">对象边界约束下的深度融合与重建</h3>

融合单目深度、LiDAR 测量与 SAM 3 对象边界后，桥梁立柱和顶部横梁呈现出较连续的表面形态，轨道与桥梁主体的相对位置清晰可辨。对象内部的分片残差校正与像素反投影，将稀疏测量扩展为带有图像颜色的三维表面采样，展示了从图像输入到对象约束重建的完整过程。

<figure id="railway-figure-4" style="margin: 1.75rem 0 0">
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 20rem), 1fr)); gap: 1.5rem; align-items: start">
<div style="min-width: 0">
    <a href="{{ '/assets/img/railway-reconstruction/results/rgb.png' | relative_url }}" target="_blank" rel="noopener" aria-label="查看原图：铁路桥梁 RGB 输入图像">
      <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/railway-reconstruction/results/rgb.png' | relative_url }}" width="1278" height="537" loading="lazy" alt="铁路桥梁 RGB 输入图像">
    </a>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">（a）RGB 图像</p>
  </div>
<div style="min-width: 0">
    <a href="{{ '/assets/img/railway-reconstruction/results/monocular-depth.png' | relative_url }}" target="_blank" rel="noopener" aria-label="查看原图：铁路桥梁单目深度预测的颜色可视化">
      <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/railway-reconstruction/results/monocular-depth.png' | relative_url }}" width="1278" height="533" loading="lazy" alt="铁路桥梁单目深度预测的颜色可视化">
    </a>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">（b）单目深度可视化</p>
  </div>
<div style="min-width: 0">
    <a href="{{ '/assets/img/railway-reconstruction/results/object-mask.png' | relative_url }}" target="_blank" rel="noopener" aria-label="查看原图：桥梁对象分割掩膜叠加在 RGB 图像上">
      <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/railway-reconstruction/results/object-mask.png' | relative_url }}" width="1227" height="538" loading="lazy" alt="桥梁对象分割掩膜叠加在 RGB 图像上">
    </a>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">（c）对象分割叠加</p>
  </div>
<div style="min-width: 0">
    <a href="{{ '/assets/img/railway-reconstruction/results/fused-cloud.png' | relative_url }}" target="_blank" rel="noopener" aria-label="查看原图：融合单目深度与 LiDAR 几何约束后的三维点云">
      <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/railway-reconstruction/results/fused-cloud.png' | relative_url }}" width="880" height="403" loading="lazy" alt="融合单目深度与 LiDAR 几何约束后的三维点云">
    </a>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">（d）深度与 LiDAR 几何融合</p>
  </div>
  </div>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 4.</strong> RGB 图像、单目深度、对象分割与融合后的三维点云。</figcaption>
</figure>

<figure id="railway-figure-5" style="margin: 1.75rem 0 0">
<div style="min-width: 0">
    <a href="{{ '/assets/img/railway-reconstruction/results/boundary-reconstruction.png' | relative_url }}" target="_blank" rel="noopener" aria-label="查看原图：对象边界约束下重建的桥梁立柱、横梁、轨道及周围植被">
      <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/railway-reconstruction/results/boundary-reconstruction.png' | relative_url }}" width="824" height="364" loading="lazy" alt="对象边界约束下重建的桥梁立柱、横梁、轨道及周围植被">
    </a>
  </div>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 5.</strong> 对象约束重建结果，展示桥梁立柱、横梁及轨道区域的三维表面形态。</figcaption>
</figure>

</section>

<section aria-labelledby="railway-views" style="margin-top: 3.5rem" markdown="1">
<h3 id="railway-views" style="font-size: 1.25rem; margin-bottom: 1rem">多视角场景展示</h3>

重建场景支持从不同方向浏览桥梁与周边环境。前向俯视展示轨道沿桥梁延伸的走向及横梁的排列，侧向视角呈现立柱、横梁与地面的空间关系，使交通设施的整体布局和构件形态直观可见。

<figure id="railway-figure-6" style="margin: 1.75rem 0 0">
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 20rem), 1fr)); gap: 1.5rem; align-items: start">
<div style="min-width: 0">
    <a href="{{ '/assets/img/railway-reconstruction/results/front-view.png' | relative_url }}" target="_blank" rel="noopener" aria-label="查看原图：铁路桥梁重建点云的前向俯视视角">
      <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/railway-reconstruction/results/front-view.png' | relative_url }}" width="831" height="462" loading="lazy" alt="铁路桥梁重建点云的前向俯视视角">
    </a>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">（a）前向俯视</p>
  </div>
<div style="min-width: 0">
    <a href="{{ '/assets/img/railway-reconstruction/results/side-view.png' | relative_url }}" target="_blank" rel="noopener" aria-label="查看原图：铁路桥梁重建点云的侧向观察视角">
      <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/railway-reconstruction/results/side-view.png' | relative_url }}" width="672" height="474" loading="lazy" alt="铁路桥梁重建点云的侧向观察视角">
    </a>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">（b）侧向观察</p>
  </div>
  </div>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 6.</strong> 铁路桥梁重建结果的前向俯视与侧向展示。</figcaption>
</figure>

</section>

<section aria-labelledby="railway-assets" style="margin-top: 3.5rem" markdown="1">
<h3 id="railway-assets" style="font-size: 1.25rem; margin-bottom: 1rem">交通资产点云提取</h3>

轨道区域与横梁点云可按类别从完整场景中提取并独立显示。提取后的轨道保留了沿线路延伸的形态，横梁以分离的构件集合呈现，实现了从整体场景浏览到交通资产检索与展示的转换。

<figure id="railway-figure-7" style="margin: 1.75rem 0 0">
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 20rem), 1fr)); gap: 1.5rem; align-items: start">
<div style="min-width: 0">
    <a href="{{ '/assets/img/railway-reconstruction/results/rail-extraction.png' | relative_url }}" target="_blank" rel="noopener" aria-label="查看原图：点云浏览界面中单独提取显示的轨道区域">
      <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/railway-reconstruction/results/rail-extraction.png' | relative_url }}" width="1172" height="453" loading="lazy" alt="点云浏览界面中单独提取显示的轨道区域">
    </a>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">（a）轨道区域提取</p>
  </div>
<div style="min-width: 0">
    <a href="{{ '/assets/img/railway-reconstruction/results/crossbeam-extraction.png' | relative_url }}" target="_blank" rel="noopener" aria-label="查看原图：点云浏览界面中按类别提取显示的多个横梁构件">
      <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/railway-reconstruction/results/crossbeam-extraction.png' | relative_url }}" width="1174" height="478" loading="lazy" alt="点云浏览界面中按类别提取显示的多个横梁构件">
    </a>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">（b）横梁提取</p>
  </div>
  </div>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 7.</strong> 从重建场景中独立提取的轨道区域与横梁点云。</figcaption>
</figure>

</section>

<section aria-labelledby="railway-frames" style="margin-top: 3.5rem" markdown="1">
<h3 id="railway-frames" style="font-size: 1.25rem; margin-bottom: 1rem">按帧浏览与观测追溯</h3>

点云浏览界面支持按来源帧选择和组合显示局部场景，保留三维点云与采集观测之间的关联。结合类别选择，可在整体场景、局部帧和交通构件之间切换，查看不同观测位置下的桥梁结构及多帧叠加效果。

<figure id="railway-figure-8" style="margin: 1.75rem 0 0">
  <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 20rem), 1fr)); gap: 1.5rem; align-items: start">
<div style="min-width: 0">
    <a href="{{ '/assets/img/railway-reconstruction/results/frame-selection-a.png' | relative_url }}" target="_blank" rel="noopener" aria-label="查看原图：第一种来源帧选择状态下的局部桥梁点云">
      <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/railway-reconstruction/results/frame-selection-a.png' | relative_url }}" width="1058" height="516" loading="lazy" alt="第一种来源帧选择状态下的局部桥梁点云">
    </a>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">（a）帧选择状态一</p>
  </div>
<div style="min-width: 0">
    <a href="{{ '/assets/img/railway-reconstruction/results/frame-selection-b.png' | relative_url }}" target="_blank" rel="noopener" aria-label="查看原图：另一种来源帧选择状态下的局部桥梁点云">
      <img class="img-fluid rounded border d-block mx-auto" style="width: 100%; height: auto; background: white" src="{{ '/assets/img/railway-reconstruction/results/frame-selection-b.png' | relative_url }}" width="1176" height="471" loading="lazy" alt="另一种来源帧选择状态下的局部桥梁点云">
    </a>
    <p class="text-muted small" style="margin: 0.65rem 0 0; line-height: 1.6">（b）帧选择状态二</p>
  </div>
  </div>
  <figcaption class="text-muted small" style="margin-top: 0.85rem; line-height: 1.6"><strong>Figure 8.</strong> 按来源帧选择与组合显示的局部桥梁点云。</figcaption>
</figure>

</section>

</section>

</article>

</div>
