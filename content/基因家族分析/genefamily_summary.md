---
title: Genefamily_summary
subtitle:
date: 2024-10-09T11:41:40+08:00
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
  - 基因家族分析
categories:
  - 基因家族分析
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

[基因家族分析帖子](https://mp.weixin.qq.com/s/mQw3jXE3tj_Nkk-P-5yi8g)
#、基因家族基础知识与研究思路介绍
## 基因家族简介
- **基因**是染色体上一段可以发生转录的区域（内含子外显子启动子）。转录本才是基因的研究实体，转录本transcript（别名 剪切体）是由一条基因通过转录形成的一种或多种可供编码蛋白质的成熟的mRNA。一条基因通过内含子的不同剪接可构成不同的转录本。设计转录本实验可以研究内含子剪切机制、表观遗传、RNA编辑等，通常是考察一条基因对应的不同转录本的调节机制等。
- **基因家族**（gene family），是来源于同一个祖先，由一个基因通过基因重复而产生两个或更多的拷贝而构成的一组基因，它们在结构和功能上具有明显的相似性，编码相似的蛋白质产物，同一家族基因可以紧密排列在一起，形成一个基因簇，但多数时候，它们是分散在同一染色体的不同位置，或者存在于不同的染色体上的，各自具有不同的表达调控模式。
- **按功能划分**：把一些功能类似的基因聚类，形成一个家族，例如GH家族（糖苷水解酶家族）等。
- **按照序列相似程度划分**：一般将同源的基因放在一起认为是一个家族，一般使用orthoMCL进行聚类
- **motif是蛋白质分子**具有特定功能的或者作为一个独立结构域一部分相近的二级结构聚合体
>1. 序列高度相似的序列，互为同源gene，归属于一个基因家族（拷贝数目多于1）
>2. 结构域的角度来说，具有保守结构域（某个或多个）的序列，即为某个基因家族的序列（可能同时要不具有另外的某个结构域）

## 常规的基因家族分析流程
1. 确定的研究基因家族
2. 了解你研究的基因家族的特征
3. 可参考收录了基因家族特征的网站
4. 查找相关文献
5. 数据下载
> - 基因组序列信息，存储基因组序列信息的.fasta文件。还有其蛋白质序列，也是以.fasta结的文件。一般来说注释的比较好的基因组都会含有这些文件。
> - 基因组基因结构注释信息。储存基因的intron，exon，CDS,gene等坐标信息的.gff3或.gtf文件。
> - 基因家族隐马可夫模型，hmm文件
> 在这些常规的生信分析后，一般的文章还会加上一些湿实验去验证，例如不同非生物条件下基因家族的表达等(PCR为主)。

## 基因家族鉴定的工具hmmer：
> - <font color='black'>一般寻找基因家族，都可以通过保守结构域来预测，从而找到物种的某一基因家族</font>
> - <font color='black'>鉴定基因家族时，常用到的工具是hmmsearch，里面常用的算法有三种。一般我们使用--cut_tc算法对隐马可夫模型进行搜索，tc算法是使用pfam提供的hmm文件中**trusted cutoof**的值进行筛选，相对比较可靠</font>


# 同源基因的鉴定
## hmm+blast

# 共线性分析
## MCScanX
## 

## KA/KS
### [知乎解读-Ka/Ks](https://zhuanlan.zhihu.com/p/144271268)
- 遗传学中，Ka/Ks表示的是两个蛋白编码基因的非同义替换率（Ka）和同义替换率（Ks）之间的比例。这个比例可以判断是否有选择压力作用于这个蛋白质编码基因


## Motif预测
### meme 参数解析：
#-protein 待预测的为蛋白序列  
#-oc result 输出路径  
#-nostatus 不将软件计算过程输出到屏幕上  
#-time 1800000 CPU消耗时间达到<time>后停止计算  
#-mod zoops motif的分布类型  
#· oops 每个功能域在每一段序列中都会出现一次，而且只出现一次。这种模式是运算速度最快，而且最为敏感的。但是如果并不是每个序列都包含功能域，那就可能会有不正确的结果。  
#· zoops 每个功能域在每一段序列中至多只出现一次，可能不出现。这种模式运算速度较快，敏感性稍弱。  
#· anr 每个功能域在每一段序列中出现的次数不定。这种模式运算速度最慢，可能会多花十倍以上的时间。但是对于功能分布的情况完全未知的情况下，这一参数可能会有帮助  
#-nmotifs 3 检测到的motif的最大限制  
#-minw 6 motif最大长度  
#-maxw 13 motif最小长度  
#-objfun classic motif检测的函数算法  
#-markov_order 0 马尔科夫模型使用的顺序  

### Usage4Linux
```sh
meme test.fa -protein -oc test -nostatus -time 18000 -mod zoops -nmotifs 10 -minw 6 -maxw 50 -objfun classic -markov_order 0
mast -oc 01Csa_meme -nostatus ./01Csa_meme/meme.xml Csa_bHLH_final.fa
```

### 安装报错
```
/public/software/env01/lib/libicui18n.so: undefined reference to `__cxa_throw_bad_array_new_length@CXXABI_1.3.8'
/public/software/env01/lib/libicui18n.so: undefined reference to `operator delete(void*, unsigned long)@CXXABI_1.3.9'
```
