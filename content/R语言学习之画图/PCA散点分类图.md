---
title: 散点分类图
subtitle:
date: 2023-06-11T21:29:47+08:00
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
### 多组数据PCA拼图-二维
{{< admonition type=abstract title="代码内容+数据结构" open=false >}}
- [x] 代码内容
```
setwd("C:/Users/90500/Desktop/tmp")
library('ggplot2')
library(ggpubr)
cycle<-list.files()
for (x in c(1:length(cycle))){
y<-strsplit(cycle[x],'\\.')[[1]][4]
print(y)
result<-read.table(cycle[x],header=T)
pca<-ggplot(result,aes(x=PC1,y=PC2,color=Subpopulation))+
  geom_point(alpha=0.8,size=3)+
  theme_bw()+
  scale_color_manual(values=c("CA"="#6495ED", "CM"="#F08080","WA"="#F4A460","WM"="#9370DB"))+
  guides(color=guide_legend(override.aes = list(size=4)))+
  ggtitle(y) +
  theme(axis.text= element_text(size= 15,face="bold"),
  axis.title = element_text(size = 15,face = "bold"),
  axis.line=element_line(size=0.8,color="black"),
  panel.border=element_blank(),
  panel.grid.major=element_blank(),
  panel.grid.minor=element_blank(),
  axis.line= element_line(colour = "black")
  plot.title = element_text(hjust = 0.5,vjust=0.2,face='bold',size = 20,color='black'),
  legend.position=c(0.89,0.83),
  legend.key=element_blank(),
  legend.text = element_text(size=12,face="bold"),
  legend.title =element_blank())

assign(paste("p", x, sep = ""), pca) ####assign()
}
p_all <- ggpubr::ggarrange(p2,p4,p3,p1,p5,p6,p7,p8, nrow = 2, ncol = 4, labels = c('', '', '', ''), font.label = list(color = 'black'))
print(p_all)
ggsave("PCA_multipleplots.pdf",width=20,height=8)
```
2. 数据结构
```
```
{{< /admonition >}}

  
### 单组数据PCA图-二维

{{< admonition type=abstract title="代码内容+数据结构" open=false >}}

```
setwd("C:/Users/90500/Desktop/tmp")
library(ggplot2)
library(ggpubr)
cycle<-list.files()
for (x in c(1:length(cycle))){
#y<-strsplit(cycle[x],'\\.')[[1]][4]
y<-cycle[x]
print(y)
result<-read.table(cycle[x],header=T)
pca<-ggplot(result,aes(x=PC1,y=PC2,color=Subpopulation))+
  geom_point(alpha=0.8,size=3)+
  theme_bw()+
  scale_color_manual(values=c("CA"="#6495ED", "CM"="#F08080","WA"="#F4A460","WM"="#9370DB"))+
  theme(panel.border=element_blank(),panel.grid.major=element_blank(),panel.grid.minor=element_blank(),axis.line= element_line(colour = "black"))+
  theme(axis.text= element_text(size= 15,face="bold"),axis.title = element_text(size = 15,face = "bold"))+
  theme(axis.line=element_line(size=0.8,color="black")) +
  theme(legend.key=element_blank(),legend.text = element_text(size=15,face="bold"),legend.title =element_blank()) +
  guides(color=guide_legend(override.aes = list(size=4)))+
  ggtitle(y) +
  theme(plot.title = element_text(hjust = 0.5,vjust=0.2,face='bold',size = 20,color='black'))
  theme(legend.position=c(0.89,0.83),legend.key=element_blank(),legend.text = element_text(size=12,face="bold"),legend.title =element_blank())
assign(paste("p", x, sep = ""), pca) ####assign()
}
p_all <- ggpubr::ggarrange(p1)
print(p_all)
#ggsave("test.png",width=10,height=8,dpi=300)
ggsave("test.pdf",width=8,height=6)
```
{{< /admonition >}}

### 商品种PCA图-二维
{{< admonition type=abstract title="代码内容+数据结构" open=false >}}
```
setwd("C:/Users/90500/Desktop")
library('ggplot2')
result<-read.table("35_snp_plink.pca_R.evec.txt",header=T)
pdf("commercial_raw.pdf",width=2.5,height=1.5)
pca<-ggplot(result,aes(x=PC1,y=PC2,color=Subpopulation))+
  geom_point(alpha=0.6,size=1)+
  theme_bw()+
  scale_color_manual(values = c("LB"="#006400","BY"="#008080","YJM"="#6495ED","YG"="#FA8072","XZM"="#FFA500"))+
  theme(panel.border=element_blank(),panel.grid.major=element_blank(),panel.grid.minor=element_blank(),axis.line= element_line(colour = "black"))+
  theme(axis.text= element_text(size= 5,face="bold"),axis.title = element_text(size = 5,face = "bold"))+
  theme(axis.line=element_line(size=0.8,color="black")) +
  theme(legend.key=element_blank(),legend.text = element_text(size=5,face="bold"),legend.title =element_blank()) +
  guides(color=guide_legend(override.aes = list(size=1)))
pca
dev.off()
```
{{< /admonition >}}

### 商品种PCA-三维
{{< admonition type=abstract title="代码内容+数据结构" open=false >}}
![Alt Text](/pca3d.png)
```
setwd("C:/Users/90500/Desktop")
library(scatterplot3d)
data<-read.table("TestMelon2KmSNP.pca.evec.R.txt",head=T,sep='\t',row.names= 1)
my_color <- c("#008080", "#6495ED", "#006400","#FFA500", "#FA8072")
colors <- my_color[as.numeric(as.factor(data[,4]))]
pdf('PCA_3d_mSNP.pdf',width = 6,height = 6)
s3d<-scatterplot3d(data[1:3],color=colors,pch = 16,cex.symbols = 0.8 ) 
legend('top',legend = unique(data[,4]),col =  my_color,ncol=1,
      pch = 16, inset = -0.1, xpd = TRUE, horiz = TRUE,bty='o', 
      x.intersp=1,y.intersp=0.5)

dev.off()
```
{{< /admonition >}}