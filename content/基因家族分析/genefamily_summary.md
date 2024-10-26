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

[test](/content/posts/R_Anova.md)