---
title: ggtree画进化树
subtitle:
date: 2023-07-15T11:01:01+08:00
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
### 依赖包：  
1. ggplot2
2. ggtree
3. treeio
4. dplyr
----------------------------
### 知识点:  
- geom_bar()
- scale_fill_manual()
- ggpubr::ggarrange()

### ggtree画进化树
{{< admonition type=abstract title="代码内容+数据结构" open=false >}}
- 代码内容
1. 横向图
```
setwd("C:/Users/90500/Desktop")
library(ggtree)
library(treeio)
library(ggplot2)
library(dplyr)
tree<-read.newick("TestMelon2K.min4.nwk")
group_info<-read.csv("Commercial.sample",header=F,sep="\t")
colnames(group_info)<-c("label","origin","Group")
tree1<-full_join(tree,group_info,by="label")
corlor_35<-c("#008080","#006400","#FFA500","#FA8072","#6495ED")
Commercial<-ggtree(tree1,aes(color=Group),
                   size=1.5,
                   branch.length = "none",
                   ladderize=FALSE)+
            geom_tiplab(size=2.5, aes(col=Group), 
                        hjust=1,linesize=5,angle=45,
                        offset=-0.5,align=F)+
            geom_tippoint(size=4,shape=15,aes(col=Group))+
            theme(legend.position = "top",
                  legend.key.size = unit(0.3, "inches"))+
            #layout_dendrogram()+
            ggtitle("Phylogenetic test\nMelon2K")+
            scale_color_manual(values = corlor_35 )
Commercial
ggsave("test.pdf",width = 8,height = 5)

```
2. 圈图
```
setwd("C:/Users/90500/Desktop")
library(ggtree)
library(treeio)
library(ggplot2)
library(dplyr)
tree<-read.newick("TestMelon2K.min4.nwk")
group_info<-read.csv("Commercial.sample",header=F,sep="\t")
colnames(group_info)<-c("label","origin","Group2","Group")
tree1<-full_join(tree,group_info,by="label")
corlor_35<-c("#6495ED","#9370DB","#006400","#FFA500","#F08080")
Commercial<-
  ggtree(tree1,aes(color=Group),
         size=2,layout = 'circular',
         branch.length = "none",
         ladderize=FALSE)+
  geom_tiplab2(size=3, aes(col=Group),
               fontface = "bold",
               hjust=0,#linesize=10,
               offset=1,align=F)+
  geom_tippoint(aes(col=Group),
                position = "identity",
                size=3,shape=16)+
  theme(axis.title.y=element_text(face="bold"),
        legend.position = "right",
        legend.key.size = unit(0.3, "inches"))+
  #ggtitle("Phylogenetic test\nMelon2K")+
  scale_color_manual(values = corlor_35 )
Commercial
Commercial_strip<-Commercial+ 
  geom_strip(1, 3, barsize = 3, color = "#006400", fontface = "bold",
             offset = 20, label = "LB", offset.text =3, 
             angle = 11, fontsize = 3, hjust = "center", extend = 0.3)+
  geom_strip(4, 6, barsize = 3, color = "#9370DB",fontface = "bold", 
             offset = 20, label = "BY9", offset.text =3, 
             angle = 55, fontsize = 3, hjust = "center", extend = 0.3)+
  geom_strip(7, 9, barsize = 3, color = "#6495ED",fontface = "bold", 
             offset = 20, label = "BY7", offset.text =3, 
             angle = -45, fontsize = 3, hjust = "center", extend = 0.3)+
  geom_strip(10,12,barsize = 3, color = "#FFA500",fontface = "bold",
             offset = 20, label = "XZM", offset.text=3,
             angle = 55, fontsize = 3, hjust = "center", extend = 0.3)+
  geom_strip(13,15,barsize = 3, color = "#F08080",fontface = "bold",
             offset = 20, label = "YG", offset.text=3,
             angle = 45, fontsize = 3, hjust = "center", extend = 0.3) 
#Commercial_strip+
Commercial+
  theme(legend.position='right',legend.key.size =unit(5,'mm'))+
  scale_shape_discrete(name  ="Group")
ggsave("test.pdf",width =6,height = 6)
system("explorer.exe test.pdf")

```
- 数据格式
1. file.nwk
```
(((((((((((((((YJM-1:0.00045760,YJM-6:0.00000000)1.0000:0.00784572,BY6:0.00000000)0.7460:0.00464967,BY61-2:0.00000000)0.5110:0.00127155,BY61-1:0.00000000)0.4020:0.00054722,BY61:0.00000000)0.2260:0.00010796,(BY94:0.00072266,BY98:0.00009634)0.0240:0.00011721)0.1600:0.00081387,BY9-9:0.00008359)0.3620:0.00092086,BY9-4:0.00000000)0.1390:0.00037640,(BY83:0.00000000,((BY7:0.00221626,BY93:0.00000000)0.3460:0.00079566,(YJM-5:0.00000000,(BY71:0.00385762,BY72:0.00000000)0.8820:0.00504447)0.4610:0.00207605)0.2170:0.00094292)0.1910:0.00081379)0.0950:0.00016540,BY9-6:0.00008983)0.3190:0.00137586,BY91:0.00000000)0.5650:0.00554379,BY8:0.00000000)0.5950:0.00515680,(BY54:0.00000000,(BY51:0.00000000,(BY55:0.00183704,(LB-3:0.00001227,(LB-1:0.00010111,LB-2:0.00000000)0.4830:0.00036282)0.4440:0.00049733)0.3780:0.00043559)0.9200:0.00554470)0.6540:0.00781420)0.6600:0.01193016,YJM-2:0.00000000)0.7940:0.01409819,BY9-5:0.00000000,(YG-1:0.00000000,(YG-3:0.01679339,(YG-2:0.01692632,(XZM-5:0.02742932,(XZM-3:0.00000000,(XZM-6:0.00000000,(XZM-1:0.00114366,XZM-2:0.00000000)0.4820:0.00145171)0.3440:0.00038670)0.9630:0.01613010)0.9960:0.03485480)0.8460:0.02561458)0.9520:0.02133085)1.0000:0.31202475);
``` 
2. group.file
```
BY51  CA  BY  BY5
BY54  CA  BY  BY5
BY55  CA  BY  BY5
BY6 CA  BY  BY6
BY61-1  CA  BY  BY6
BY61-2  CA  BY  BY6
BY61  CA  BY  BY6
BY7 CA  BY  BY7
BY71  CA  BY  BY7
BY72  CA  BY  BY7
BY8 CA  BY  BY8
BY83  CA  BY  BY8
BY91  CA  BY  BY9
BY93  CA  BY  BY9
BY94  CA  BY  BY9
BY9-4 CA  BY  BY9
BY9-5 CA  BY  BY9
BY9-6 CA  BY  BY9
BY98  CA  BY  BY9
BY9-9 CA  BY  BY9
LB-1  CA  LB  LB
LB-2  CA  LB  LB
LB-3  CA  LB  LB
XZM-1 CM  XZM XZM
XZM-2 CM  XZM XZM
XZM-3 CM  XZM XZM
XZM-5 CM  XZM XZM
XZM-6 CM  XZM XZM
YG-1  CM  YG  YG
YG-2  CM  YG  YG
YG-3  CM  YG  YG
YJM-1 CA  YJM YJM
YJM-2 CA  YJM YJM
YJM-5 CA  YJM YJM
YJM-6 CA  YJM YJM
``` 
{{< /admonition >}}