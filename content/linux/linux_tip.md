---
title: Linux_tip
subtitle:
date: 2023-07-09T16:45:08+08:00
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
  - linux
categories:
  - linux
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
## [Linux文本搜索引擎](https://tools.yeefire.com/linux-command-man/list.html#!kw=)  
### sed
- 
- 批量删除所有提交的任务  
`qstat |sed '1,2d' |cut -f1|cut -d "." -f1 | xargs qdel`
- sed 批量替换多个字符串  
`sed -i -e '1,$s///g' -e '1,$s///g' -e '1,$s///g' `
- tr命令用于转换或删除文件中的字符所有换行符换成','最后一个分隔符','替换为换行符 #列转行 #  
`cat file.txt |tr "\n" ","|sed -e 's/,$/\n/'` 
- sed 打印2-4行
`sed -n '1,4p'`
### awk
- awk中的条件判断式  
`awk '{if() print $0}' `  
`awk '$1 !~ /#/ {print}' # ~ !~ `  
- awk替换某一列为特定字符  
`awk 'sub($1,"str")' file`  
`awk '{$1="str";print}' file`  
- awk tip  
`awk '{ for(i=2;i<=NF;i++) { if(i<NF){printf"%s",$i"\t"} else{print $i"\t"} } }' file #打印第一列以外的其他列`  
`awk '{for(i=0;++i<=NF;)a[i]=a[i]?a[i] FS $i:$i}END{for(i=0;i++<NF;)print a[i]}' #行转列`  

### grep
### 零零散散
- 更改任务的时间  
`qalter PID -l walltime=10:00:00`  
- 查看内存  
`beegfs-ctl --getquota --uid --all `  
- 节点上线程处理（需要查）
`ps ux`  
`jobs -l`  
`kill -9 pid`  
- sort tip  
`sort -k 3nr -t $'\t' `