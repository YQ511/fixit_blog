---
title: "基因组注释"
date: 2023-05-30T11:33:54+08:00
draft: false
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
  - 基因组注释
categories:
  - 基因组注释
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

# [基因组注释参考帖](https://liuyujie0136.gitbook.io/sci-tech-notes/bioinformatics/genome-denovo-ann)
### 重复注释 {#RepeatAnnotation}
1. 重复序列广泛存在于真核生物基因组中, 这些重复序列或集中成簇,或分散在基因之间。根据分布把重复序列分为散在重复序列和串联重复序列。  
2. 重复序列根据序列特征分为2类：串联重复（Tandem repeats）和散布重复（Dispersed repeats）  
```
#RepeatMasker 基于Repbase(DNA)/自建Elibrary查询重复序列
#-nohow:屏蔽低复杂简单重复; -no_is:跳过细菌插入元件检查; -norna:不掩盖小RNA(伪)基因;
#-parallel 并行使用的处理器数,可提升分析速度
RepeatMasker -nolow -no_is -norna -parallel 2 -lib RepeatMasker.lib genome.fa

#RepeatProteinMask 基于 Repbase(pep)查询重复序列
#noLowSimple:关闭低复杂度和简单重复的屏蔽/注释; -pvalue:接受匹配的阈值
#注意点: genome.fa的D不能长于18个字符
RepeatProteinMask -noLowSimple -pvalue 0.0001 genome.fa

#TRF 基于元件的结构特征等来识别重复序列
trf genome.fa 2 7 7 80 10 50 2000 -d -h

#LTR-FINDER 基于重复序列特征
#-w 2 输出格式,2-table;  -C:检测中心粒,删除高重复区域
Itr_finder -W 2 -C -s tRNAs.fa genome.fa

#repeatmodeler 基于自身序列比对
#-name:创建 database的名称;
#-pa:共享内存处理器的数量程序,可提升分析速度
BuildDatabase -name mydb genome.fa
RepeatModeler -database mydb -pa 6 >run.out
```

### 结构注释 {#StructureAnnotation}
注释可以产生具有生物学功能的蛋白的基因。一般包括启动子, 转录起始, 5'UTR, 起始密码子, 外显子, 内含子, 终止密码子, 3'UTR, poly-A等结构。  
- [ ] 从头(De novo)注释  
```
augustus --species=XXX --AUGUSTUS CONFIG PATH= config --uniqueGeneld=true --nolnFrameStop=true--gff3=on --strand=both genome.mask.fa> genome.mask.fa.out 
# --uniqueGeneld=true:gene:命名 aseqname.gn; 
# --nolnFrameStop=true:不带有终止密码子的转录本; 
# --gff3=on:输出格式gff3 
glimmerhmm.genome.mask.fa -d XXX- f -g genome.mask.fa.gff
# -d 库de路径;
# -f:不要partial gene predictions;
# -g输出格式gff
# 真核,预测的基因数目较多长度较短,一般用于植物
```
- [ ] 转录组注释  

- [ ] 同源注释  

- [ ] Iso注释  

### 非编码RNA注释 {#ncRNAAnnotation}
| 非编码RNA类型 | 功能 | 策略 |
| :--- | :---- | :---- |
| rRNA/核糖体RNA | 与蛋白质结合形成核糖体,其功能是作为mn的支架,提供mRNA翻译成蛋白质的场所| 采用与已有的全长rRNA进行blastn比对而获得|
| tRNA/转运RNA | 携带氨基酸进入核糖体,使之在mRNA指导下合成蛋白质 |使用tRNAscan-SE对三叶草型二级结构进行检测|
| miRNA | 将mRNA降解或抑制其翻译,具有沉默基因的功能 |采用Rfam和INFERNAL进行二级结构检测|
| SnRNA/小核RNA | 主要参与RNA前体的加工过程,是RNA剪切体的主要成分 |上同|
### MAKERE整合 {#Structure Annotation}
```
maker maker_exe.ctl maker_opts.ctl maker_bopts.ctl
#maker exe.ct:执行程序的路径
#maker_ boots.ctl: BLAST7和 Exonerate的过滤参数
#maker opts.ctl:其他信息,例如输入基因组文件,主要调整输入文件等( genome= ;est= ;protein= ;pred_gff= ;)
```
### 功能注释 {#Structure Annotation}
| 常用数据库 | 软件 | 参考贴 |
| :----: | :----: | :----: |
| [基因功能注释数据库(GeneOntology)](http://www.geneontology.org/) | InterProScan|  |
| [Interpro](http://www.ebi.ac.uk/interpro/) | InterProScan |  |
| [Uniprot(SWISS-PROT,TrEMBL)](http://www.uniprot.org/) | blastp |  |
| [KEGG:生物学通路数据库(Gene,Pathway,Ligand)](http://www.genome.jp/kegg/) | blastp |  |

### 基因组评估BUSCO {#Structure Annotation}
1. 基于python语言，对转录组和基因组组装质量进行评估  
2. BUSCO就是使用相近的物种之间的保守序列与组装的结果进行比对，鉴定组装的结果是否包含这些序列，包含单条、多条还是部分或者不包含等等情况来给出结果。  
3. BUSCO软件根据OrthoDB数据库, 构建了几个大的进化分支的单拷贝基因集。将其与该基因集进行比较, 根据比对上的比例、完整性, 来评价准确性和完整性。  


