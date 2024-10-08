---
title: Transposon
subtitle:
date: 2024-09-28T16:06:11+08:00
draft: false
type: posts
author:
  name:
  link:
  email:
  avatar:
description:
keywords:
license:
comment: false
weight: 0
tags:
  - 转座子
categories:
  - 转座子
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

# See details front matter: https://fixit.lruihao.cn/documentation/content-management/introduction/#front-matter
---

> 转座现象是指一段DNA序列可以从原位上单独复制或断裂下来，环化后插入另一位点，并对其后的基因起调控作用。这段序列称为“跳跃基因”或转座子。

- 专业英语：
1. synapsis：n.染色体结合，染色体联会
2. Vitro Transposition: 体外转座
3. cleavage：n.劈开，分裂
4. assay: n.化验；试验
5. transposase: 转座酶
6. hyperactive： adj.极度活跃的；活动过度的
7. dimerization: n.二聚, 二聚作用 (有机化学)
- 知识点补充：
1. 多肽的N端（氮端）在最左边，多肽的C端（碳端）在最右边。
2. 脱水缩合：氨基酸分子结合的方式是由一个氨基酸分子的羧基（—COOH）和另一个氨基酸分子的氨基（—NH2）结合连接，同时脱去一分子水，这种结合方式叫做脱水缩合。连接两个氨基酸分子的（—NH—CO—）其中左数的第二个“—”是叫做肽键的化学键，具有部分双键性质。
### 转座的分类
> 一般来说，根据转座方式的不同，将转座子分为“Ⅰ型转座子”和“Ⅱ型转座子”。
- Ⅰ型转座子：“复制-粘贴”模式，RNA polⅡ将转座子DNA转录为mRNA，再反转录为cDNA，最后在整合酶催化下将其整合到基因组上的新位置。
- Ⅱ型转座子：“剪切-粘贴”模式，在转座酶的作用下，Ⅱ型转座子从原来位置上解离下来，重新整合到染色体上。常**应用于NGS领域的Tn5，也属于此类转座子**。

### Tn5
- Tn5转座子是一种细菌转座子，最早从E. coli大肠杆菌中发现，Tnp序列全长477个氨基酸。
- Tn5 Tnp含有三个结构域：N末端、催化结构域和C末端。其中N末端包含70个氨基酸，组成许多α螺旋和β-转角用于DNA binding；Tnp活性中心位于中间300个氨基酸，包含一个“核糖核酸酶H样基序”、一个混有β片层结构的α/β/α折叠结构；C端完全由α螺旋组成，主要负责蛋白质-蛋白质相互作用。
- Tn5转座复合体是一个同源二聚体，是由两个Tnp识别OE序列后二聚化，然后剪切供体DNA后形成的。
### [Tn5转座子的性质](https://zhuanlan.zhihu.com/p/643068502)
> Tn5序列主要包含四个组分：
1. IS50  
  - IS50R和IS50L的序列高度同源。IS50R上的Tnp和Inh分别编码转座酶（Tnp）和转座抑制因子（Inh），Inh可与Tnp形成多聚体复合物进而抑制Tnp介导的转座；IS50L上的P3和P4则分别编码Tnp和Inh的无功能形式。
2. Outside end（OE） sequences
  - OE序列由19个碱基组成，可被Tnp所识别，参与整个Tn5的转座。
3. Inside end（IE） sequences  
  - IE序列不参与Tn5的转座（OE-OE），仅参与IS50的转座（IE-OE）。
4. Drug resistance genes  
  - Tn5上的耐药基因主要有kan、str和ble。  
<p align = 'center'>
<img src="/转座结构示意图.jpg" width="500">  
</p>

[Tn5 in Vitro Transposition](https://www.sciencedirect.com/science/article/pii/S0021925818617053)  
A. the features critical for Tn5 transposition include the transposase (Tnp), the inhibitor of transposition (Inh), and the 19-bp end sequences (the outside end, OE, and the inside end, IE). The P3 and P4 proteins are nonfunctional versions of Tnp and Inh. A more detailed description of Tn5 can be found in Refs.3 and 15.    
B. hyperactive Tnp mutations used in this study.    
C. 19 bp outside end sequence.    

### 转座机理
- 转座发生时，两个Tnp识别结合Tn5转座子两端的OE序列，形成Tnp-OE复合物，然后两个Tnp-OE复合物通过C端介导互作并形成具有切割DNA能力的Tn5转座复合体。随后Tn5转座复合体利用切割活性，经过一系列化学反应切除供体DNA，离开供体链。当结合到靶DNA上时，复合体识别并攻击靶序列（Target site），将转座子插入到靶序列中，粘性末端通过DNA聚合酶、连接酶作用进行填补，两端形成9bp正向重复序列。整个转座过程完成了基因从原始DNA被剪切之后粘贴在另一受体DNA的过程，实现了基因的“跳跃”。

### Tn5的前沿应用
1. ATAC-seq
> Assay for Transposase - Accessible Chromatin with highthroughput sequencing  
- 利用高通量测序检测转座酶易接近的染色质的技术。真核生物的核DNA紧密缠绕在组蛋白周围，并经过进一步的折叠、浓聚形成染色体。当DNA进行复制或转录时，折叠结构会被打开形成可接近的区域，ATAC-seq技术利用Tn5转座酶切割暴露的DNA，使其连接上特异性的Adapters，插入Adapters的DNA片段可被分离出来用于二代测序，从而获得大量的细胞系和组织样本基因表达、转录调控、转录修饰等的信息。相对其他如MNase-seq，FAIRE-seq和DNase-seq等染色质研究方法来说，ATAC-seq具有快速、样本需求量少、一次性获得全基因组上的染色质开放区域等优势，在表观遗传学具有广阔的发展前景。
2. LIANTI
> Linear Amplification via Transposon Insertion
- 通过转座子插入线性扩增，是一项经过改良的单细胞全基因组扩增（Whole-genome Amplification, WGA）方法。利用Tn5转座酶结合LIANTI序列，形成含有T7 promoter的Tn5转座复合体，复合体结合到单细胞基因组DNA，将DNA随机片段化并插入LIANTI转座子。通过T7 promoter的体外转录，获得大量线性扩增的转录本，然后经过逆转录得到大量的扩增产物，随后进行建库测序操作。整个过程仅进行线性扩增，没有进行指数扩增，大大增强了扩增稳定性，降低PCR干扰，此外，该技术使得测量拷贝数的空间分辨率提高了3个数量级（能在千碱基分辨率进行微CNV检测，基因组覆盖率可达到97%），助力更有效、更精准地检测出更多遗传疾病。