---
title: Pandas
subtitle:
date: 2023-07-16T16:14:06+08:00
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
  - Python
categories:
  - Python
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

# Pandas包的使用细则

1. 文件的读取
- `read_csv('infile.csv',sep='\t',header=None))`
| 常用参数 | 详解 |
| :---| :---- |
| header=None | 第一行不设置为表头 |
| sep='\t' | 读取后以制表符分割 |
2. 文件的输出
- `df.to_csv('outfile.csv',sep='\t',index=False,na_rep='NA')`
| 参数 | 详解 |
| :---| :---- |
| index=False | 输出格式不带有索引列 |
| na_rep='NA' | 缺失的元素以'NA'表示 |
3. dict转成df格式
- `pd.DataFrame([dict])`
3. 数据结构(DataFrame,df)切片提取特定索引的列或行
- 提取前四列：`df.iloc[:,:4]`;提取前四行：`df.iloc[:4,:]`
4. df: 一维表二维表的转换
`stack()`  
`unstack()`
2. DataFrame打印  
- `df.to_string(index = False)`  
`df.to_string(buf=None, columns=None, col_space=None, header=True, index=True, na_rep=’NaN’, formatters=None, float_format=None, index_names=True, justify=None, max_rows=None, max_cols=None, show_dimensions=False, decimal=’.’, line_width=None)
`  
- `pd.option_context()`  
- `pd.set_option()`  
- `pd.to_markdown()`  
