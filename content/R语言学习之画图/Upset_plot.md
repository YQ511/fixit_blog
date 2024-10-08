---
title: Upset_plot
subtitle:
date: 2024-03-25T16:39:52+08:00
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
  - R语言绘图
categories:
  - R语言绘图
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
# 用途
1. 展示多个集合之间的交叠关系，且很容易从图中看出集合之间的交集信息
2. 比如不同组织或不同时期表达基因间的交集关系
### 参考贴
#### [UpSetR-参考贴一](https://zhuanlan.zhihu.com/p/370210775)  
{{< admonition type=abstract title=TestCode >}}
```R

```
{{< /admonition >}}  

#### [ComplexUpset-参考贴二](https://www.jianshu.com/p/9753f6c938fe)
{{< admonition type=abstract title=TestCode >}}

```R
library(ggplot2)
library(ComplexUpset)

movies <- as.data.frame(ggplot2movies::movies)
head(movies, 3)
genres <- colnames(movies)[18:24]
genres
movies[movies$mpaa == "", "mpaa"] <- NA
movies <- na.omit(movies)
upset(movies,genres,
      name = "genres", # 底部的标签
      width_ratio = 0.1 # 左侧图形的宽度
      )
```
{{< /admonition >}}

#### [ggupset-参考贴三 通过Upset进行实验设计分组](https://blog.csdn.net/weixin_45822007/article/details/121413844)