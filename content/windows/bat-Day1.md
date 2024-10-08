---
title: Bat Day1
subtitle:
date: 2023-08-09T09:06:16+08:00
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
  - windows脚本
categories:
  - windows脚本
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

# 批处理(bat)命令学习第一天
### 注释命令之rem和::命令
- 任何以冒号:开头的字符行,在批处理中都被视作标号, 而直接忽略其后的所有内容。
1. 有效标号：冒号后紧跟一个以字母数字开头的字符串，goto 语句可以识别。
2. 无效标号：冒号后紧跟一个非字母数字的一个特殊符号，goto 无法识别的标号，可以起到注释作用，所以`::`常被用作注释符号，其实`:`也可起注释作用
- 与rem不同的是, :: 后的字符行在执行时不会回显, 无论是否用echo on打开命令行回显状态, 因为命令解释器不认为他是一个有效的命令行, 就此点来看, rem 在某些场合下将比 :: 更为适用; 另外, rem 可以用于 config.sys 文件中。

示例
```bat
@echo off
python check.py > check.txt
pause
exit
rem randome write
```