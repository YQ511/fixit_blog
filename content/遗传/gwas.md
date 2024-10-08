---
title: GWAs
subtitle:
date: 2024-08-27T20:30:31+08:00
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
  - 遗传学
categories:
  - 遗传学
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
## Emmax

## [GCTA](https://yanglab.westlake.edu.cn/software/gcta/#Overview)

## LeadSNP
```sh
bFile=/public/agis/huangsanwen_group/yuqing/.tmp/workspace_1/tomato/GWAsV3/data_geno/SL3.0.snp.plink
function clump(){
echo "SNP       P" > $@_pvalue.ps.clump
cat $@_pvalue.ps|cut -f1,3|sed '1,$s/:/_/g' >> $@_pvalue.ps.clump
plink --bfile ${bFile} --out $@_pvalue.ps.clump --clump $@_pvalue.ps.clump \
        --clump-kb 1000 --clump-r2 0.2 \
        --clump-p1 2.92E-7 \
        --clump-p2 2.92E-7
rm $@_pvalue.ps.clump.log $@_pvalue.ps.clump.nosex
cat $@_pvalue.ps.clump.clumped|
}
clump $1

```

## [PVE-变异解释率](https://www.omicsclass.com/article/2406#:~:text=PVE%20%28phenotypic,variation%20explained%29%EF%BC%8C%E6%98%AF%E6%8C%87%E8%A1%A8%E5%9E%8B%E5%8F%98%E5%BC%82%E8%A7%A3%E9%87%8A%E7%8E%87%EF%BC%8C%E5%8D%B3%E7%AD%89%E4%BD%8D%E5%8F%98%E5%BC%82%E5%8F%AF%E4%BB%A5%E5%9C%A8%E5%A4%9A%E5%A4%A7%E7%A8%8B%E5%BA%A6%E4%B8%8A%E5%BD%B1%E5%93%8D%E8%A1%A8%E5%9E%8B%EF%BC%8C%E8%BF%99%E4%B8%AASNP%E8%A7%A3%E9%87%8A%E4%BA%86%E8%A1%A8%E5%9E%8B%E6%96%B9%E5%B7%AE%E7%9A%84%E7%99%BE%E5%88%86%E4%B9%8B%E5%A4%9A%E5%B0%91%E3%80%82)

## LD

## Fst