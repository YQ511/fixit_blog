---
title: "Piecharts"
date: 2023-06-07T14:53:16+08:00
subtitle:
draft: false ##turn on/off 
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
---
# plot by R code
1. [R语言数据可视化饼图](https://zhuanlan.zhihu.com/p/80415566)
2. [ggplot绘制饼图](https://zhuanlan.zhihu.com/p/80415566)
3. [R语言调色板](https://zhuanlan.zhihu.com/p/546088806)
```
library(ggplot2)
library(dplyr)
col<-c("#6495ED","#008B8B","#3CB371", 
       "#DAA520", "#D2691E","#8B0000", 
       "#DA70D6")
p <- group_by(mpg, class) %>%
  summarise(percent = n() / nrow(mpg)) %>%
  ggplot(aes(x = factor(1), y = percent, fill = class)) +
  geom_col(colour = "white")
p + coord_polar(theta = "y", start = 1.65) +
  scale_fill_brewer(palette="Set3")+
  #scale_fill_manual(values=col)+
  geom_text(aes(label = paste0(round(percent*100, 2), "%")), 
            position = position_fill(vjust = 0.5)) +
  theme(panel.background = element_blank(),
        axis.title = element_blank(),
        axis.text = element_blank(),
        axis.ticks = element_blank()
        )

```