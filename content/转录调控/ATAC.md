---
title: ATAC
subtitle:
date: 2024-11-30T16:41:06+08:00
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
  - 转录调控
categories:
  - 转录调控
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

# [一文详解ATAC-seq原理+读图：表观遗传的秀儿](https://zhuanlan.zhihu.com/p/512163334)
&emsp; 感谢知乎作者科研忍者老熊提供ATAC的解读，本帖主要依据此贴进行梳理学习
<hr style="border-top: 5px solid black;">
# 前言知识点

> 基因的转录，是需要将DNA的高级结构解开的，但不是需要DNA链全部解开，只需要打开一部分，也就是表达基因的区域解开即可。而这一过程，主要由<font color="darkred"><b>染色体组蛋白的修饰（尤其是乙酰化）</b></font>来实现的，这部分打开的染色质，就叫<font color="darkred"><b>开放染色质（open chromatin）</b></font>。而染色质一旦打开，就允许一些调控蛋白（比如转录因子）跑过来与之相结合。染色质的这种特性，就叫做<font color="darkred"><b>染色质的可及性（chromatin accessibility）</b></font>，所以说染色质的可及性反映的就是调控因子与开放染色质结合的状态，与转录调控密切相关。

## 如何利用ATAC-seq去找开放的染色质区域呢？

- 转座酶Tn5：DNA转座是一种由DNA转座酶介导，把DNA序列从染色体的一个区域插入到另外一个区域的现象，类似于“剪切粘贴”。这个过程，也是需要插入位点的染色质是开放的，否则就会被一大坨高级结构给卡住。
- 既然转座酶Tn5容易结合在开放染色质上，只要人为地将将NGS接头连接到转座酶，携带这些接头的转座酶（如下图带着红色蓝色测序标签的转座酶Tn5）进入细胞核后，在染色质开放区域各种切切切，使染色质断裂并将这些接头插入到开放的染色质区域中，这样我们裂解细胞、破碎DNA后，利用已知序列的测序标签进行NGS测序，就知道哪些区域是开放染色质了。

## ATAC-seq和ChIP-seq有啥区别？

- ChIP-Seq：实验前明确有一个感兴趣的转录因子，根据目标转录因子设计抗体去做ChIP实验拉DNA，验证感兴趣的转录因子是否与DNA存在相互作用；

- ATAC-Seq：没有落脚到具体哪个转录因子，是在全基因组范围内检测染色质的开放程度，可以得到全基因组范围内的蛋白质可能结合的位点信息，用这个技术方法与其他方法结合是想去筛感兴趣的调控因子。

> 实际上，在全基因组上检测染色质开放程度用<font color="darkred"><b>DNase-Seq、ATAC-Seq、FAIRE-Seq、MNase-seq</b></font>都可以，他们又有什么区别呢？

- MNase-seq和DNase-Seq是用MNase或DNase I内切酶识别开放染色质区域，把切割完的DNA测序，和已知的全基因组序列进行比对，就知道被切掉了哪里，哪里没有被切掉，从而检测出开放的染色质区域。但是实验费时费力，重复性差；

- FAIRE-Seq是先进行超声裂解，然后用酚-氯仿富集，不依赖酶和抗体，但弊端就是检测背景高，测序信噪比低，甲醛交联时间不好把握等等；

- 相比起来，ATAC-seq是用Tn5转座酶，操作起来也更加简单，重复性好，而且最重要的一点是实验只需要很少的细胞/组织量，出来的信号也更加漂亮，所以ATAC-seq目前已经是研究染色质开放性首选的技术方法。

## 基本概念

> &emsp; 核小体是由<font color="darkred"><b>DNA和组蛋白</b></font>形成的<font color="darkred"><b>染色质基本结构单位</b></font>。每个核小体由146bp的DNA缠绕组蛋白八聚体1.75圈形成。核小体核心颗粒之间通过50bp左右的连接DNA相连。H1结合在盘绕在八聚体上的DNA双链开口处，核小体的形状类似一个扁平的碟子或一个圆柱体，此时DNA的长度压缩7倍，称染色质纤维。染色质就是由一连串的核小体所组成。当一连串核小体呈螺旋状排列构成纤丝状时，DNA的压缩包装比约为40。纤丝本身再进一步压缩后，成为常染色质的状态时，DNA的压缩包装比约为1000。有丝分裂时染色质进一步压缩为染色体，压缩包装比高达8400，即只有伸展状态时长度的万分之一。  
>> &emsp; 核小体是染色质的基本结构单位，由<font color="darkred"><b>H2A、H2B、H3和H4等4种组蛋白(histone，H）</b></font>构成。两分子的H2A、H2B、H3和H4形成一个组蛋白八聚体，约200 bp的DNA分子盘绕在组蛋白八聚体构成的核心结构外面1.75圈形成了一个核小体的<font color="darkred"><b>核心颗粒</font></b>（core particle）。核小体的核心颗粒再由DNA（约60bp）和组蛋白H1共同构成的连接区连接起来形成串珠状的染色质细丝。这时染色质的压缩包装 比（packing ratio）为6左右，即DNA由伸展状态压缩了近6倍。200 bpDNA为平均长度；不同组织、不同类型的细胞，以及同一细胞里染色体的不同区段中，盘绕在组蛋白八聚体核心外面的DNA长度是不同的。如真菌的可以短到只有154 bp，而海胆精子的可以长达260bp，但一般的变动范围在180bp到200bp之间。在这 200bp中，146 bp是直接盘绕在组蛋白八聚体核心外面，这些DNA不易被核酸酶消化，其余的DNA是用于连接下一个核小体。连接相邻2个核小体的DNA分子上结合了另一种组蛋白H1。组蛋白H1包含了一组密切相关的蛋白质，其数量相当于核心组蛋白的一半，所以很容易从染色质中抽提出来。所有的H1被除去后 也不会影响到核小体的结构，这表明H1是位于蛋白质核心之外的。

## 常见的染色质开放区有哪些呢？

- 常见的染色质开放区主要是基因上游的启动子和远端的调控元件比如增强子和沉默子，启动子是靠近转录起始点(TSS)的DNA区域，它包含转录因子的结合位点（transcription factor binding site，TFBS），所以转录因子能够结合在启动子上TFBS，招募RNA聚合酶进而转录基因。增强子一般位于启动子下游或上游1Mb的DNA区域，转录因子与增强子结合，并与启动子区域接触时，能够促进基因的转录。相反，沉默子会减少或抑制基因的表达。

- 所以说，ATAC-seq可以帮助识别启动子区域、潜在的增强子或沉默子，也就是说，ATAC-seq中的peak，往往是启动子、增强子序列，以及一些反式调控因子结合的位点。

## ATAC-seq归根结底能用来干什么？

> <font color='darkred' size=5;><b>鉴定重要转录因子：</b></font>

&emsp; 根据原理可以知道，ATAC所捕获染色质开放区一般是正在转录的那部分DNA序列的上下游，得到这些序列我们就可以对富集到的序列结合motif分析，识别哪种转录因子参与了基因表达调控，最常见的就是去研究转录因子结合的启动子区域（对于抗体质量不好的转录因子，尤其有效）

> <font color="darkred" size=5;><b>生成转录因子结合区域的特征(footprinting)：</b></font>

&emsp; 转录因子结合在DNA上后，它占有的空间阻碍了转座酶Tn5酶切在其他无核小体区域，这样就会留下一个一个小区域，称为足迹（footprint），在这些区域中，reads由高覆盖率峰值突然下降。所以ATAC-seq footprints可以帮助我们查看转录因子在全基因组上结合的状态，主要应用于研究细胞重编程机制，染色质重塑因子，表观修饰对疾病的作用域、T细胞耗竭等等。

> <font color="darkred" size=5;><b> 生成表观基因组图谱</b></font>

> <font color="darkred" size=5;><b> 得到在不同组织或不同条件下对应可及性区域</b></font>

> <font color="darkred" size=5;><b> 得到核小体位置</b></font>

## [表观组学中的motif分析到底在研究什么？  ](https://zhuanlan.zhihu.com/p/471350610)

&emsp; 在各类表观组学文章中，motif分析总是占据着关键版面，例如m6A文章中经典的RRACH类型RNA甲基化motif、ATAC文章中各类转录因子结合位点预测也少不了motif结果的展示，甚至可以利用motif分析预测蛋白功能。用途如此广泛的分析究竟该如何去理解与学习其基础概念，手上有数据该如何完成此类分析，分析结果又如何解读，今天我们就带大家来好好认识一下这位期刊文章中的常客—motif分析。  

&emsp; motif（模体）这个概念很早就被提出，而首次系统化描述这个概念内容的文章是在2002年，发表于Science期刊上。在这篇文章中，motif被定义为：在复杂网络中某种连接模式出现频率显著高于随机网络的现象。

---


<hr style="border-top: 5px solid black;">
<p align="center"><font size=5><b>分割线</b></font></p>
<hr style="border-top: 5px solid black;">


## ATAC数据处理及可视化 
### From fastq to peakcalling

### From Peak calling to visualization