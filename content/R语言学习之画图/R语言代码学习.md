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
## 记录积累R中的常规命令
```
.libPaths() #列出R的路径
list.files() #列出当前工作路径的所有文件
getwd() #获取当前工作路径 
setwd("PATH") #设置工作路径（目录）
rm(list = ls()) #清除所有的变量
ls() #显示所有变量
capabilities() #显示支持的设备
names() #列出变量名
write.table(x,file="",row.names = FALSE,col.names = FALSE,quote = FALSE,sep='\t') #x：写入对象，file：输出对象，row/col.names：行名和列名是否输入，quote：索引是否输入，sep：分割“字符”,append:追加输入(TRUE)删除后输入(FALSE)
```
###
- 基于某一列的数值生成重复行
```R
data<-read.table('取样记录表.txt')
idx <- rep(1:nrow(data), times = data[,4]) 
result<-data[idx,]
```
### R语言中的循环
#### 判断
`x<-80`  
`x<-80L`  
`class(x)`  
`is.numeric(x)`  
#### if语句
```R
x<-c('apples','banana','pear')
if('one'%in%x){ # %in%唯一匹配
  print('1')
}else if('apple'%in%x){
  print('2')
}else {
  print('3')
}
grepl('apple',x) # 模糊匹配
any(grepl('apple',x)) # any()返回向量中任意为TRUE则为RUE
```
#### for语句
```R
v<-LETTERS[1:7]
nct<-0
for (x in v) {
  nct=nct+1
  if(nct%%2==1){
  print(paste(x,nct,sep='-'))
  }
}
```
#### While语句
```R
while(TRUE){
  print('Okay')
}
```

### excel文件xlsx的读取和写入
```R
library('openxlsx') #加载包
df<-read.xlsx('example.xlsx',sheet="Sheet1") #读取xlsx文件的sheet1表格
wb<-createWorkbook() #创建工作簿
addWorksheet(wb,"sheet1") #添加工作sheet表
writeData(wb,'sheet1',result) #写入变量内容
saveWorkbook(wb,file="取样记录表.xlsx",overwrite = T) #保存xlsx文件
```

### R包的安装
R包版本的查看：  
`packageVersion("")`
#### install.packages()
```R
install.packages() #安装包
```
#### BiocManager
```R
install.packages("BiocManager")
BiocManager::install("")
```
#### Devtools
```R
devtools::install_github("")
```
#### 源码安装
1. R cmd
```R
packageurl <- "https://cran.r-project.org/src/contrib/Archive/limma/limma_1.8.10.tar.gz" # 安装1.8.10版本的limma
install.packages(packageurl, repos=NULL, type="source")
```
2. Linux cmd
```sh
wget https://cran.r-project.org/src/contrib/Archive/limma/limma_1.8.10.tar.gz
R CMD INSTALL limma_1.8.10.tar.gz
```
#### remote安装
```R
if(!requireNamespace("remotes", quietly=TRUE)){
    install.packages("remotes")
}
remotes::install_github("YuLab-SMU/ggtreeExtra")
```