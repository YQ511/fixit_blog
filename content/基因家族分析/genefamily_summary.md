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
[基因家族分析帖子](https://www.jianshu.com/p/ae320da46b29)
# Title:基因家族基础知识与研究思路介绍 
## 一、基因家族简介
- **基因**是染色体上一段可以发生转录的区域（内含子外显子启动子）。转录本才是基因的研究实体，转录本transcript（别名 剪切体）是由一条基因通过转录形成的一种或多种可供编码蛋白质的成熟的mRNA。一条基因通过内含子的不同剪接可构成不同的转录本。设计转录本实验可以研究内含子剪切机制、表观遗传、RNA编辑等，通常是考察一条基因对应的不同转录本的调节机制等。
- **基因家族**（gene family），是来源于同一个祖先，由一个基因通过基因重复而产生两个或更多的拷贝而构成的一组基因，它们在结构和功能上具有明显的相似性，编码相似的蛋白质产物，同一家族基因可以紧密排列在一起，形成一个基因簇，但多数时候，它们是分散在同一染色体的不同位置，或者存在于不同的染色体上的，各自具有不同的表达调控模式。
- **按功能划分**：把一些功能类似的基因聚类，形成一个家族，例如GH家族（糖苷水解酶家族）等。
- **按照序列相似程度划分**：一般将同源的基因放在一起认为是一个家族，一般使用orthoMCL进行聚类
- **motif是蛋白质分子**具有特定功能的或者作为一个独立结构域一部分相近的二级结构聚合体
>1. 序列高度相似的序列，互为同源gene，归属于一个基因家族（拷贝数目多于1）
>2. 结构域的角度来说，具有保守结构域（某个或多个）的序列，即为某个基因家族的序列（可能同时要不具有另外的某个结构域）

## 二、常规的基因家族分析流程
1. 确定的研究基因家族
2. 了解你研究的基因家族的特征
3. 可参考收录了基因家族特征的网站
4. 查找相关文献
5. 数据下载
> - 基因组序列信息，存储基因组序列信息的.fasta文件。还有其蛋白质序列，也是以.fasta结的文件。一般来说注释的比较好的基因组都会含有这些文件。
> - 基因组基因结构注释信息。储存基因的intron，exon，CDS,gene等坐标信息的.gff3或.gtf文件。
> - 基因家族隐马可夫模型，hmm文件
> 在这些常规的生信分析后，一般的文章还会加上一些湿实验去验证，例如不同非生物条件下基因家族的表达等(PCR为主)。

## 三、基因家族鉴定及分析

### 3.1 同源基因的鉴定
#### 3.1.1 参考基因组和注释文件下载
> 去物种各自官网进行下载
- 基因组、蛋白以及注释文件下载好后：
1. 到对下载好的蛋白质序列进行筛选和过滤，保留序列最长的代表性转录本。 
2. 将所有的数据都纳入到分析里面，然后最后进行过滤，剔除一个基因的其他转录本。
3. 帖子：在做玉米的MYB的时候，发现代表性转录本里面其实并不包含MYB Domain，而是其他转录本包含了MYB Domain。
> [拟南芥数据库](https://www.arabidopsis.org/download/overview)
> [水稻数据库](http://rice.uga.edu/) 
> [Phytozome 数据库](https://phytozome-next.jgi.doe.gov/)
#### 3.1.2 hmm文件的下载

 [Interproscan|Pfam检索蛋白家族(pfam)](https://www.ebi.ac.uk/interpro/) 
   
<div style="text-align: center;">
    <img src="/基因家族hmm文件的下载.jpg" width="1000" alt="hmm文件的下载">
</div>

#### 3.1.3 hmm之TBtools

<div style="text-align:center;">
  <img src="/基因家族之TBtools进行hmmsearch.png" width="500" alt="TBtools进行hmmsearch">
</div>

#### 3.1.4 hmm之hmmsearch命令行
1.  [参考贴](https://mp.weixin.qq.com/s?__biz=MzU2OTkyMTExMQ==&mid=2247486322&idx=1&sn=e4f4cacf32b0b10b2d36c266a471f79e&chksm=fcf6104acb81995c399a687ed919fb43e06fd01fe3c67404a729e72dc0b99bd4621d8df97574&scene=21#wechat_redirect)
> - <font color='black'>一般寻找基因家族，都可以通过保守结构域来预测，从而找到物种的某一基因家族</font>
> - <font color='black'>鉴定基因家族时，常用到的工具是hmmsearch，里面常用的算法有三种。一般我们使用--cut_tc算法对隐马可夫模型进行搜索，tc算法是使用pfam提供的hmm文件中**trusted cutoof**的值进行筛选，相对比较可靠</font>
- hmm基因查询
```sh
## 参数解析：--noali --cpu --domtblou -domE 
hmmsearch --noali --cpu 2 --domtblout ./${i}/${i}_bHLH.tblout -o ./${i}/${i}_bHLH.stout -E 0.01 --domE 0.01 PF00010.hmm ../02_Blast/${i}_pep.fa
```
- 生成seed文件并建立新的hmm模型并进行新的一轮hmmsearch
```sh
hmmalign -o ./${k}/${k}_bHLH.cyc${c}.seed PF00010.hmm ./${k}/${k}_bHLH_domain.fa
hmmbuild ./${k}/${k}_bHLH.cyc${c}.hmm ./${k}/${k}_bHLH.cyc${c}.seed
hmmsearch --noali --cpu 2 --domtblout ./${k}/${k}_bHLH.cyc${c}.tblout -o ./${k}/${k}_bHLH.cyc${c}.stout -E 0.01 --domE 0.01 ./${k}/${k}_bHLH.cyc${c}.hmm ../02_Blast/${k}_pep.fa
```
#### 3.1.5 Blast
[参考贴](https://mp.weixin.qq.com/s?__biz=MzU2OTkyMTExMQ==&mid=2247486359&idx=1&sn=6e6fa99982f378a632d20198cdbcf8a1&chksm=fcf610afcb8199b976852f282b9f86536ac0bd174e61a27a26e548a25190d71e4a16c4867dea&cur_album_id=3508258733375717382&scene=189#wechat_redirect)
- 其他物种中基因家族的获取  
  >以拟南芥为例
    1. [从拟南芥官网进行基因家族文件的下载](https://www.arabidopsis.org/download/)
    <div style="text-align: center;">
     <img src="/基因家族之拟南芥基因家族文件信息的下载.png" width="500" alt="拟南芥基因家族文件的下载">
    </div>
    2. 提取拟南芥中目的基因家族的基因ID并提取序列
- 建库/比对
```sh
makeblastdb -in pep.fa -dbtype prot -out pep.db
blastp -db pep.fa -query AT_bHLH.fa -out species.gf.blast -max_target_seqs 5 -outfmt 6 -evalue 1e-3 -num_threads 10;
```
- 输出文件的提取

#### 3.1.6 对Hmm和Blast进行验证
[参考贴](https://mp.weixin.qq.com/s?__biz=MzU2OTkyMTExMQ==&mid=2247486371&idx=1&sn=10385667ddbf4f1a3f3de6a79dadc749&chksm=fcf6109bcb81998d962590937899e9ad1f097406ad38117413a04658c411e03dd4e10fe25fa1&cur_album_id=3508258733375717382&scene=189#wechat_redirect)
- 通过cat进行基因合并

- 结构域鉴定
```sh
wget -c ftp://ftp.ebi.ac.uk:21/pub/databases/Pfam/current_release/Pfam-A.hmm.gz
wget -c  ftp://ftp.ebi.ac.uk:21/pub/databases/Pfam/current_release/Pfam-A.hmm.dat.gz
wget -c ftp://ftp.ebi.ac.uk:21/pub/databases/Pfam/current_release/active_site.dat.gz
gunzip *.gz
hmmpress Pfam-A.hmm
hmmscan -o scan.out --tblout scan.tbl --domtblout scan.dom --noali -E 1e-5 Pfam-A.hmm Cu.blast.hmm.wrky.fa
#grep 'PF03106' scan.dom|awk '{print $4}'|sort|uniq > scan.idseqkit
seqkit grep -n -f scan.idseqkit ChineseLong_pep_v3.fa > scan.pep.pfam.wrky.fa
#python get_geneinfo_by_id.py --arg1 scan.idseqkit --arg2 ChineseLong_v3.gff3 --arg3 scan.pep.pfam.wrky.gene_info.out
Rscript pep_characteristic.r scan.pep.pfam.wrky.fa
```
- 家族成员蛋白质特征的获取
```R
library(tidyverse)
library(Biostrings)
library(Peptides)
library(ggfun)
library(ggbeeswarm)
library(patchwork)
library(ggprism)
library(writexl)
####----load Data----####
# sequence
fa <- readAAStringSet("./pfam_scan.id.pep.fa")

pep_df <- data.frame(fa) %>%
  rownames_to_column("ID") %>% 
  dplyr::mutate(Length = Peptides::lengthpep(seq = fa)) %>%  # lengthpep() 计算长度
  dplyr::mutate(MW = mw(seq = fa)) %>%                 # mw() 计算分子量
  dplyr::mutate(hydrophobicity = hydrophobicity(seq = fa)) %>%     # hydrophobicity() 计算疏水性
  dplyr::mutate(pI = pI(seq = fa)) %>%                 # pI() 计算等电点
  as_tibble() 
write_xlsx(pep_df, path = "pfam_scan_info.xlsx")
```

#### 3.1.6 CDD数据库和SMART数据库的验证
> [CDD数据库对蛋白文件进行验证](https://www.ncbi.nlm.nih.gov/Structure/bwrpsb/bwrpsb.cgi)  

> SMART数据库对蛋白文件的验证 


### 3.2 基因组共线性分析
#### MCScanX
MCScanX是检测基因共线性和进化分析的常用工具之一，2012发表至今引用数200+，作者之一的唐海宝老师是国内植物基因组学生信分析、软件开发领域的大拿，在学习使用MCScanx之前推荐先看看他08年介绍gene synteny和collinearity概念的science文章以及MCScanX软件算法文章。
>- Tang H, Bowers J E, Wang X, et al. Synteny and Collinearity in Plant Genomes[J]. Science, 2008, 320(5875):486-488.
>- Wang Y, Tang H, DeBarry JD, Tan X, Li J, Wang X, Lee TH, Jin H, Marler B, Guo H, Kissinger JC, Paterson AH. (2012) MCScanX: a toolkit for detection and evolutionary analysis of gene synteny and collinearity. Nucleic Acids Res, 40(7): e49.
- 输入文件的准备
1. 基因组间Blast比对结果文件：种内和种间共线性
2. gff文件前四列：染色体、基因号、起始、终止
- 对物种对进行MCScanX共线性分析：gff、blast和文件夹命名需要一致且在同一个文件夹里
```sh
MCScanX ${i}_pep -e 1e-5
```

### 3.3 KA/KS分析
1. [知乎解读-Ka/Ks](https://zhuanlan.zhihu.com/p/144271268)
2. 遗传学中，Ka/Ks表示的是两个蛋白编码基因的非同义替换率（Ka）和同义替换率（Ks）之间的比例。这个比例可以判断是否有选择压力作用于这个蛋白质编码基因


### 3.4 Motif预测分析
[进化树_结构域_motif_基因结构](https://mp.weixin.qq.com/s?__biz=MzU2OTkyMTExMQ==&mid=2247486515&idx=1&sn=51deab09e8766bd0908f0dc4d9394d7e&chksm=fcf6170bcb819e1d0193e1efe95cba36d24b1e281ca4fa83757a382a73034f88d4d8aa7af8a3&scene=21#wechat_redirect)
#### motif预测

```sh
meme test.fa -protein -oc test -nostatus -time 18000 -mod zoops -nmotifs 10 -minw 6 -maxw 50 -objfun classic -markov_order 0
mast -oc 01Csa_meme -nostatus ./01Csa_meme/meme.xml Csa_bHLH_final.fa
```
- 参数解析：  
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

#### 安装报错
```
/public/software/env01/lib/libicui18n.so: undefined reference to `__cxa_throw_bad_array_new_length@CXXABI_1.3.8'
/public/software/env01/lib/libicui18n.so: undefined reference to `operator delete(void*, unsigned long)@CXXABI_1.3.9'
```

### 3.5 进化树分析
- 所需软件：muscle; iqtree
```sh
muscle -align ../../input/05_tree/scan.pep.pfam.wrky.fa -output ../../output/05_tree/pfam_scan.id.pep.muscle
iqtree -s ../../output/05_tree/pfam_scan.id.pep.muscle -m MFP -bb 1000 -bnni  -nt AUTO  -cmax 15  -redo 
```

### 3.6 基因家族的染色体分布图

### 3.6 蛋白质互作

### 3.7 GO功能注释+KEGG通路注释

### 3.8 转录组热图

### 3.9 orthofinder鉴定直系同源基因
> [orthofinder 帖子](https://lxz9.com/2021/11/18/OrthoFinder/#:~:text=%E4%BB%8B%E7%BB%8D%20OrthoFinder,%E6%98%AF%E4%B8%80%E4%B8%AA%E5%BF%AB%E9%80%9F%E3%80%81%E5%87%86%E7%A1%AE%E5%92%8C%E5%85%A8%E9%9D%A2%E7%9A%84%E6%AF%94%E8%BE%83%E5%9F%BA%E5%9B%A0%E7%BB%84%E5%AD%A6%E5%B9%B3%E5%8F%B0%E3%80%82%20%E5%AE%83%E6%89%BE%E5%88%B0%E6%AD%A3%E4%BA%A4%E7%BE%A4%28orthogroups%29%E5%92%8C%E7%9B%B4%E7%B3%BB%E5%90%8C%E6%BA%90%28orthologs%29%EF%BC%8C%E6%8E%A8%E6%96%AD%E6%89%80%E6%9C%89%E6%AD%A3%E4%BA%A4%E7%BE%A4%E7%9A%84%E6%9C%89%E6%A0%B9%E5%9F%BA%E5%9B%A0%E6%A0%91%EF%BC%8C%E5%B9%B6%E8%AF%86%E5%88%AB%E8%BF%99%E4%BA%9B%E5%9F%BA%E5%9B%A0%E6%A0%91%E4%B8%AD%E7%9A%84%E6%89%80%E6%9C%89%E5%9F%BA%E5%9B%A0%E5%A4%8D%E5%88%B6%E4%BA%8B%E4%BB%B6%E3%80%82%20%E5%AE%83%E8%BF%98%E4%B8%BA%E8%A2%AB%E5%88%86%E6%9E%90%E7%9A%84%E7%89%A9%E7%A7%8D%E6%8E%A8%E6%96%AD%E5%87%BA%E4%B8%80%E4%B8%AA%E6%9C%89%E6%A0%B9%E7%9A%84%E7%89%A9%E7%A7%8D%E6%A0%91%EF%BC%8C%E5%B9%B6%E5%B0%86%E5%9F%BA%E5%9B%A0%E5%A4%8D%E5%88%B6%E4%BA%8B%E4%BB%B6%E4%BB%8E%E5%9F%BA%E5%9B%A0%E6%A0%91%E6%98%A0%E5%B0%84%E5%88%B0%E7%89%A9%E7%A7%8D%E6%A0%91%E7%9A%84%E5%88%86%E6%94%AF%E3%80%82)
> [orthofinder 帖子](https://blog.csdn.net/u012110870/article/details/115511929)
> [orthofinder 帖子](https://www.jianshu.com/p/2b460949a1c8)
### 3.10 cafe进行基因家族收缩与扩张

> [收缩与扩张帖子](https://phantom-aria.github.io/2023/12/01/a.html)