---
title: R语言之常规代码
subtitle:
date: 2023-07-15T15:33:36+08:00
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

<!--more-->
### 记录积累R中的常规命令
```
.libPaths() #列出R的路径
list.files() #列出当前工作路径的所有文件
getwd() #获取当前工作路径 
setwd("PATH") #设置工作路径（目录）
rm(list = ls()) #清除所有的变量
ls() #显示所有变量
install.packages() #安装包
capabilities() #显示支持的设备
names() #列出变量名
write.table(x,file="",row.names = FALSE,col.names = FALSE,quote = FALSE,sep='\t') #x：写入对象，file：输出对象，row/col.names：行名和列名是否输入，quote：索引是否输入，sep：分割“字符”,append:追加输入(TRUE)删除后输入(FALSE)
```