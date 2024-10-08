---
title: ANOVA
subtitle:
date: 2024-09-02T11:08:31+08:00
type: posts
draft: false
author:
  name: YQ
  link:
  email: 905008171@qq.com
  avatar:
description:
keywords:
license:
comment: false
weight: 0
tags:
  - R语言学习之统计分析
categories:
  - R语言学习之统计分析
hiddenFromHomePage: false
hiddenFromSearch: false
summary:
resources:
  - name: featured-image
    src: featured-image.jpg
  - name: featured-image-preview
    src: featured-image-preview.jpg
toc: true
math: false
lightgallery: false
password:
message:
repost:
  enable: true
  url:

---

# [方差分析](https://www.zhihu.com/tardis/zm/art/296726829?source_id=1005)
&emsp; ANOVA，Analysis of Variances，又叫变异数分析，主要功能是“检验两个或多个样本的平均数的差异是否显著”。其本质是：  

&emsp; 分析样本的组间变异程度（方差）和组内变异程度相比，是否足够大。如果够大，证明这个分组因素，对于样本均值的影响是显著的。
F检验。ANOVA由F检验实现，因此某些场合也被称为F检验。