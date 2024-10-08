---
title: 绘图之ggplot
subtitle:
date: 2023-10-31T11:43:42+08:00
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

### 图片格式(字体，大小，坐标轴，背景)
{{< admonition type=abstract title="ggplot画图格式" open=false >}}
```
1. 坐标轴
labs(x=" ",y=" ") #X和Y的坐标轴标题
scale_x_continuous(expand=expansion(add = c(0.7,0.7)),limits=c(-10,5)) #X轴和Y轴的刻度范围
scale_y_continuous(expand=expansion(add = c(0.5,0.5)),limits=c(-7.5,5)) # X轴和Y轴的刻度范围
axis.line=element_line(size=0.7,color="black")) #坐标轴线
axis.text.x =element_text(angle=45,vjust=0.6) #x轴的坐标轴刻度字
axis.text = element_text(size= 15,face="bold") #所有的坐标轴刻度字
axis.ticks = element_line(colour="black") #刻度线的颜色，尺寸
axis.title = element_text(size = 15,face = "bold") #坐标轴标题的字设置
2. 字体
theme_bw(base_size=20) #改变图片中整体字体的大小
3. 标题
ggtitle(y) #绘图标题
theme(plot.title = element_text(size=15,hjust=0.5)) #将绘图标题调整到中间
4. 图例
legend.position=c(0.89,0.83) #图例位置
legend.key=element_blank() #图例背景
legend.text = element_text(size=12,face="bold") #图例字体
legend.title =element_blank() #图例标题
```
{{< /admonition >}}


### 添加组间显著性标识
{{< admonition type=abstract title="ggplot2显著性" open=false >}}
```
library(ggsignif)
geom_signif(comparisons = list(c("A", "B"),c("A", "C"),c("B", "C")),
              y_position = c(4, 4.8, 4.2),map_signif_level = TRUE)
```
{{< /admonition >}}              

### 颜色填充
{{< admonition type=abstract title="ggplot2颜色填充" open=false >}}
```
scale_fill_manual(values=c("#DC143C","#6495ED","#F08080","#F4A460","#9370DB")) #
scale_color_manual(name="", values = c("#e26fff","#8e9cff")) #

```
{{< /admonition >}}    

### [y轴截断 truncation](https://zhuanlan.zhihu.com/p/558355764)
