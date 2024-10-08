---
title: Blup
subtitle:
date: 2024-03-11T19:26:40+08:00
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
1. BLUP（Best Linear Unbiased Prediction）最佳线性无偏预测
lmer函数用于拟合线性混合模型，然后通过ranef函数提取随机效应，即BLUP值。
<!--more-->
```R
library("lme4")
```

### Blup计算代码(source='WYY')
  需要学习和测验
```R
library("lme4")

setwd("//Users/wuyaoyao//work//03-evolutionary-dele//05-Deleterious//03-fitness")
tuber.dat = read.table("Tuber.weight_wp-2019.8.27_yyw.perl.plant.csv", header=T,sep=",")
data.num=0
ID_transfor=read.table("/Users/wuyaoyao/work/02-potato/02-deleterious\ mutation/03_Potato.deleterious.mutation/02-367_genotype_lianqun/name_list_group.infor",header=T)
tuber.dat$PG=ID_transfor$id[match(tuber.dat$C_ID,ID_transfor$C_ID)]
write.table(tuber.dat,"Tuber.weight_wp-2019.8.27_yyw.perl.plant.txt",quote=F,sep="\t",row.name=F)

tuber.dat_with.data=tuber.dat[apply(tuber.dat[,2:6],1,function(x) sum(!is.na(x)))>data.num,]
write.table(tuber.dat_with.data,"Tuber.weight_wp-2019.8.27_yyw.perl.plant_with.at.least.one.weight.txt",quote=F,sep="\t",row.name=F)

tuber.weight_multi=stack(tuber.dat_with.data[,c(2:6)])
tuber.weight_multi$Line=rep(tuber.dat_with.data$C_ID,ncol(tuber.dat_with.data)-2)
tuber.weight_multi=cbind(tuber.weight_multi,t(matrix(unlist(strsplit(as.character(tuber.weight_multi[,2]),split = "_")),nrow=2)))
names(tuber.weight_multi)=c("tuber.weight","Env","Line","Loc","Year")

#brixmodel = lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Year) + (1|Rep%in%Loc:Year) + (1|Line:Loc) + (1|Line:Year))

biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Year) + (1|Line:Loc) + (1|Line:Year),data=tuber.weight_multi)

> summary(biomass.model)
> summary(biomass.model)
Linear mixed model fit by REML ['lmerMod']
Formula: tuber.weight ~ (1 | Line) + (1 | Loc) + (1 | Year) + (1 | Line:Loc) +  
  (1 | Line:Year)
Data: tuber.weight_multi

REML criterion at convergence: -448.9

Scaled residuals: 
  Min      1Q  Median      3Q     Max 
-3.9600 -0.2354 -0.0599  0.1553  5.5229 

Random effects:
  Groups    Name        Variance  Std.Dev.
Line:Year (Intercept) 0.0022158 0.04707 
Line:Loc  (Intercept) 0.0374722 0.19358 
Line      (Intercept) 0.0104607 0.10228 
Year      (Intercept) 0.0002902 0.01703 
Loc       (Intercept) 0.0040693 0.06379 
Residual              0.0090646 0.09521 
Number of obs: 1435, groups:  
  Line:Year, 1011; Line:Loc, 1008; Line, 510; Year, 3; Loc, 3

Fixed effects:
  Estimate Std. Error t value
(Intercept)  0.21840    0.03922   5.568
> 
  
Vg :Line的variance: 0.0104607
VGL ：Line x locationa variance 0.0374722
VGY: Line x Year variance: 0.0022158
Ve : residual variance: 0.0090646
h2=vg/((vg+vgl/L+vgy/y+(vgLy/(L*y)) * (ve/(L*y*g)))
h2=0.0104607/(0.0104607+ 0.0022158/3+ 0.0374722/3+ 0.0090646/5)
0.410176

biomass.blup = ranef(biomass.model)$Line
write.table(biomass.blup,"Tuber-weight-from_per.plant_510.lines.blup.csv",quote=F,sep=",")

sum(row.names(biomass.blup)==tuber.dat_with.data$C_ID)
tuber.dat_with.data$biomass.510.blup= biomass.blup
sum(biomass.blup<0) #336
sum(biomass.blup>0)#174
tuber.dat_with.data$mean=apply(tuber.dat_with.data[,2:6],1,mean,na.rm=T)
write.table(tuber.dat_with.data,"./blup/Tuber.weight_wp-2019.8.27_yyw.perl.plant_with.at.least.one.weight.txt",quote=F,sep="\t",row.name=F)
pheno_cor=cor(tuber.dat_with.data[,-c(1,7)],use="pairwise.complete.obs")
write.table(pheno_cor,"./blup/Tuber.weight_wp-2019.8.27_yyw.perl.plant_with.at.least.one.weight_cor.between.rep.txt",quote=F,sep="\t",row.name=T)
#230.lines
lines230=read.table("/Users/wuyaoyao/work/02-potato/02-deleterious mutation/03_Potato.deleterious.mutation/02-367_genotype_lianqun/Potato_deleterious.mutation.stastics_230candolleanum.landrances.txt",header=T)
lines230$C_ID=match(lines230)
tuber.weight_multi$PG=ID_transfor$id[match(tuber.weight_multi$Line,ID_transfor$C_ID)]
tuber.weight_multi_230=tuber.weight_multi[!is.na(match(tuber.weight_multi$PG,lines230$homo.line)),]
tuber.weight_multi_230$Line=factor(tuber.weight_multi_230$Line,levels=as.character(unique(tuber.weight_multi_230$Line)))
 
biomass.model_230 = lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Year) + (1|Line:Loc) + (1|Line:Year),data=tuber.weight_multi_230)
> summary(biomass.model_230)
Linear mixed model fit by REML ['lmerMod']
Formula: tuber.weight ~ (1 | Line) + (1 | Loc) + (1 | Year) + (1 | Line:Loc) +      (1 | Line:Year)
Data: tuber.weight_multi_230

REML criterion at convergence: -947.2

Scaled residuals: 
  Min      1Q  Median      3Q     Max 
-2.0493 -0.4009 -0.1252  0.2662  4.8571 

Random effects:
  Groups    Name        Variance  Std.Dev.
Line:Year (Intercept) 1.142e-03 0.03380 
Line:Loc  (Intercept) 5.747e-03 0.07581 
Line      (Intercept) 3.300e-03 0.05745 
Year      (Intercept) 1.392e-05 0.00373 
Loc       (Intercept) 3.170e-03 0.05630 
Residual              7.077e-03 0.08412 
Number of obs: 708, groups:  Line:Year, 485; Line:Loc, 469; Line, 218; Year, 3; Loc, 3

Fixed effects:
  Estimate Std. Error t value
(Intercept)  0.18444    0.03333   5.533
h2= 3.300e-03/(3.300e-03+1.142e-03/3+5.747e-03/3+7.077e-03/5)
0.4706397

biomass.blup_230 = ranef(biomass.model_230)$Line
sum(biomass.blup_230[,1]<0 #149
    
tuber.dat_with.data$biomass.blup_218=biomass.blup_230[match(tuber.dat_with.data$C_ID,row.names(biomass.blup_230)),1]

write.table(tuber.dat_with.data,"./blup/Tuber.weight_wp-2019.8.27_yyw.perl.plant_with.at.least.one.weight.txt",quote=F,sep="\t",row.name=F)
pheno_cor=cor(tuber.dat_with.data[,-c(1,7)],use="pairwise.complete.obs")
write.table(pheno_cor,"./blup/Tuber.weight_wp-2019.8.27_yyw.perl.plant_with.at.least.one.weight_cor.between.rep.txt",quote=F,sep="\t",row.name=T)


tuber.weight_multi_230_field= tuber.weight_multi_230[tuber.weight_multi_230$Loc!="Yingmao",]
tuber.weight_multi_230_field$Env=factor(tuber.weight_multi_230_field$Env,levels=as.character(unique(tuber.weight_multi_230_field$Env)))
tuber.weight_multi_230_field$Loc=factor(tuber.weight_multi_230_field$Loc,levels=as.character(unique(tuber.weight_multi_230_field$Loc)))
tuber.weight_multi_230_field$Year=factor(tuber.weight_multi_230_field$Year,levels=as.character(unique(tuber.weight_multi_230_field$Year)))
#biomass.model_230_field = lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Year) + (1|Line:Loc) + (1|Line:Year),data=tuber.weight_multi_230_field)

#####230 field data

fit_s = lmer(tuber.weight ~ (1|Line) + (1|Env),data=
tuber.weight_multi_230_field[tuber.weight_multi_230_field$Line %in% selected_lines,])
re <- ranef(fit_s, condVar=TRUE)
u <- re$Line
pev <- attr(u, "postVar")[1,1,]
s2_u <- VarCorr(fit_s)$Line[1,1]
r <- 1-pev/s2_u
mean(r)
summary(fit_s)
##########################################################
#230 
fit_230= lmer(tuber.weight ~ (1|Line) + (1|Env),
 data=tuber.weight_multi_230)
re <- ranef(fit_230, condVar=TRUE)
u <- re$Line
pev <- attr(u, "postVar")[1,1,]
s2_u <- VarCorr(fit_230)$Line[1,1]
r <- 1-pev/s2_u
mean(r) #0.4974263
summary(fit_230)
h2=0.6374715

###at least 3 data in 230 lines
{
#Env model
tab=table(na.omit(tuber.weight_multi_230)$Line)
selected_lines <-  names(tab)[tab >= 3] #145
fit_230_3.data= lmer(tuber.weight ~ (1|Line) + (1|Env),data=
               tuber.weight_multi_230[tuber.weight_multi_230$Line %in% selected_lines,])
re <- ranef(fit_230_3.data, condVar=TRUE)
u <- re$Line
pev <- attr(u, "postVar")[1,1,]
s2_u <- VarCorr(fit_230_3.data)$Line[1,1]
r <- 1-pev/s2_u
mean(r)
summary(fit_230_3.data)
######### Loc Year model
fit_230_3.data= lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Year) + (1|Line:Loc) + (1|Line:Year)
,data=tuber.weight_multi_230[tuber.weight_multi_230$Line %in% selected_lines,])
re <- ranef(fit_230_3.data, condVar=TRUE)
u <- re$Line
pev <- attr(u, "postVar")[1,1,]
s2_u <- VarCorr(fit_230_3.data)$Line[1,1]
r <- 1-pev/s2_u
mean(r)
summary(fit_230_3.data)
}

#################################
#218 lines
{
  #Env model
    fit_230= lmer(tuber.weight ~ (1|Line) + (1|Env),data=
                         tuber.weight_multi_230)
  re <- ranef(fit_230, condVar=TRUE)
  u <- re$Line
  pev <- attr(u, "postVar")[1,1,]
  s2_u <- VarCorr(fit_230)$Line[1,1]
  r <- 1-pev/s2_u
  mean(r)
  summary(fit_230)
  ######### Loc Year model
  fit_230= lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Year) + (1|Line:Loc) + (1|Line:Year)
,data=tuber.weight_multi_230)
  re <- ranef(fit_230, condVar=TRUE)
  u <- re$Line
  pev <- attr(u, "postVar")[1,1,]
  s2_u <- VarCorr(fit_230)$Line[1,1]
  r <- 1-pev/s2_u
  mean(r)
  summary(fit_230)
}


#########
#all lines
{
  #Env model
  fit_all= lmer(tuber.weight ~ (1|Line) + (1|Env),data=
                  tuber.weight_multi)
  re <- ranef(fit_all, condVar=TRUE)
  u <- re$Line
  pev <- attr(u, "postVar")[1,1,]
  s2_u <- VarCorr(fit_all)$Line[1,1]
  r <- 1-pev/s2_u
  mean(r)
  summary(fit_all)
  ######### Loc Year model
  fit_all= lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Year) + (1|Line:Loc) + (1|Line:Year)
                ,data=tuber.weight_multi)
  re <- ranef(fit_all, condVar=TRUE)
  u <- re$Line
  pev <- attr(u, "postVar")[1,1,]
  s2_u <- VarCorr(fit_all)$Line[1,1]
  r <- 1-pev/s2_u
  mean(r)
  summary(fit_all)
}

at least 3 data in 510 lines
{
  #Env model
  tab=table(na.omit(tuber.weight_multi)$Line)
  selected_lines <-  names(tab)[tab >= 3] #149
  fit_3.data= lmer(tuber.weight ~ (1|Line) + (1|Env),data=
  tuber.weight_multi[tuber.weight_multi$Line %in% selected_lines,])
  re <- ranef(fit_3.data, condVar=TRUE)
  u <- re$Line
  pev <- attr(u, "postVar")[1,1,]
  s2_u <- VarCorr(fit_3.data)$Line[1,1]
  r <- 1-pev/s2_u
  mean(r)
  summary(fit_3.data)
  ######### Loc Year model
  fit_3.data= lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Year) + (1|Line:Loc) + (1|Line:Year)
 ,data=tuber.weight_multi[tuber.weight_multi$Line %in% selected_lines,])
  re <- ranef(fit_3.data, condVar=TRUE)
  u <- re$Line
  pev <- attr(u, "postVar")[1,1,]
  s2_u <- VarCorr(fit_3.data)$Line[1,1]
  r <- 1-pev/s2_u
  mean(r)
  summary(fit_3.data)
}


####rm 2019Campus field
tuber.weight_multi=read.table("Tuber.weight_wp-2019.8.27_stack.data.format.txt",header=T)
tuber.weight_multi_rm.Camp.2019=subset(tuber.weight_multi,Env!="Campus.field_2019")
#fit_all= lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Year) + (1|Line:Loc) + (1|Line:Year) ,data=tuber.weight_multi_rm.Camp.2019)
fit= lmer(tuber.weight ~ (1|Line) + (1|Env),data=tuber.weight_multi_rm.Camp.2019)
h2= 0.012878/(0.012878+0.033555/4)=0.6055462
blup=ranef(fit, condVar=TRUE)$Line
tuber.dat_with.data=read.table("Tuber.weight_wp-2019.8.27_yyw.perl.plant_with.at.least.one.weight.txt",header=T,sep="\t")
tuber.dat_with.data$biomass.blup_510_rm.Camp2019_Env=blup[match(tuber.dat_with.data$C_ID,row.names(blup)),1]

tab=table(na.omit(tuber.weight_multi_rm.Camp.2019)$Line)
selected_lines <-  names(tab)[tab >= 3] #149
fit_3.data= lmer(tuber.weight ~ (1|Line) + (1|Env),data= tuber.weight_multi_rm.Camp.2019[tuber.weight_multi_rm.Camp.2019$Line %in% selected_lines,])
h2=0.004078/(0.004078+0.012458/4)= 0.5669795
blup=ranef(fit_3.data, condVar=TRUE)$Line
tuber.dat_with.data$biomass.blup_510.at.least3.data_rm.Camp2019_Env=blup[match(tuber.dat_with.data$C_ID,row.names(blup)),1]


lines230=read.table("/Users/wuyaoyao/work/02-potato/02-deleterious mutation/03_Potato.deleterious.mutation/02-367_genotype_lianqun/Potato_deleterious.mutation.stastics_230candolleanum.landrances.txt",header=T)
tuber.weight_multi_230=tuber.weight_multi[!is.na(match(tuber.weight_multi$PG,lines230$homo.line)),]
tuber.weight_multi_230_rm.Camp.2019=subset(tuber.weight_multi_230,Env!="Campus.field_2019")
fit= lmer(tuber.weight ~ (1|Line) + (1|Env),data=tuber.weight_multi_230_rm.Camp.2019)
h2= 0.003300/(0.003300+0.011231/4)= 0.5402972
blup=ranef(fit, condVar=TRUE)$Line
tuber.dat_with.data$biomass.blup_230_rm.Camp2019_Env=blup[match(tuber.dat_with.data$C_ID,row.names(blup)),1]


tab=table(na.omit(tuber.weight_multi_230_rm.Camp.2019)$Line)
selected_lines <-  names(tab)[tab >= 3] #149
fit_3.data= lmer(tuber.weight ~ (1|Line) + (1|Env),data= tuber.weight_multi_230_rm.Camp.2019[tuber.weight_multi_230_rm.Camp.2019$Line %in% selected_lines,])
h2=0.004037/(0.004037+0.012684/4)=0.5600721
blup=ranef(fit_3.data, condVar=TRUE)$Line
tuber.dat_with.data$biomass.blup_230.at.least3.data_rm.Camp2019_Env=blup[match(tuber.dat_with.data$C_ID,row.names(blup)),1]


write.table(tuber.dat_with.data,"Tuber.weight_wp-2019.8.27_yyw.perl.plant_with.at.least.one.weight.txt",quote=F,sep="\t",row.name=F)
pheno_cor=(cor(tuber.dat_with.data[,-c(1,2,8,9)],use="pairwise.complete.obs"))^2
write.table(pheno_cor,"Tuber.weight_wp-2019.8.27_yyw.perl.plant_with.at.least.one.weight_cor.between.rep_R2.txt",quote=F,sep="\t",row.name=T)

all.cor.infor=NULL                                                                                             
for (i in 3:7){
  for (j in (3:7)){
    data1=tuber.dat_sift[,c(i,j)]
    Pheno=names(data1)[1]
    Dele=names(data1)[2]
    names(data1)=c("y","x")
    cor_r=(cor(data1[,1],data1[,2],use="pairwise.complete.obs"))
    cor_r2=(cor(data1[,1],data1[,2],use="pairwise.complete.obs"))^2
    line.model <- lm(y~0+x, data=data1)
    coeffi=line.model$coefficients
    pdf(paste(Pheno,Dele,".pdf",sep="_"),width=10)
    x=data1$x
    y=data1$y
    plot(x,y,xlab="Number of deleterious mutation",ylab="Tuber weight per plant",col="darkcyan",pch=16)
    #clip(min(x,na.rm=T), max(x,na.rm=T), min(y,na.rm=T), max(y,na.rm=T)+(max(y,na.rm=T)-min(y,na.rm=T))/6)
    fit.int <- lm(y~x)
    
    abline(fit.int, lwd=2, col="red")
    dev.off()
    Intercept=fit.int$coefficients[1]
    x=fit.int$coefficients[2]
    cor.infor=data.frame(Pheno,Dele,cor_r,cor_r2,coeffi,Intercept,x)
    all.cor.infor=rbind(all.cor.infor,cor.infor)
  }
}






####four data
data.num=3
tuber.dat_with.data=tuber.dat[apply(tuber.dat[,-1],1,function(x) sum(!is.na(x)))>data.num,]

tuber.weight_multi=stack(tuber.dat_with.data[,-1])
tuber.weight_multi$Line=rep(tuber.dat_with.data$C_ID,ncol(tuber.dat_with.data)-1)
tuber.weight_multi=cbind(tuber.weight_multi,t(matrix(unlist(strsplit(as.character(tuber.weight_multi[,2]),split = "_")),nrow=2)))
tuber.weight_multi$Line=factor(tuber.weight_multi$Line,levels=(as.character(unique(tuber.weight_multi$Line))))
names(tuber.weight_multi)=c("tuber.weight","Env","Line","Loc","Year")

#brixmodel = lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Year) + (1|Rep%in%Loc:Year) + (1|Line:Loc) + (1|Line:Year))

biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Year) + (1|Line:Loc) + (1|Line:Year),data=tuber.weight_multi)

 summary(biomass.model)
 Linear mixed model fit by REML ['lmerMod']
 Formula: tuber.weight ~ (1 | Line) + (1 | Loc) + (1 | Year) + (1 | Line:Loc) +  
   (1 | Line:Year)
 Data: tuber.weight_multi
 
 REML criterion at convergence: -336.3
 
 Scaled residuals: 
   Min      1Q  Median      3Q     Max 
 -3.5272 -0.2654 -0.0604  0.1894  5.9983 
 
 Random effects:
   Groups    Name        Variance  Std.Dev.
 Line:Year (Intercept) 0.0029852 0.05464 
 Line:Loc  (Intercept) 0.0346299 0.18609 
 Line      (Intercept) 0.0088989 0.09433 
 Year      (Intercept) 0.0002812 0.01677 
 Loc       (Intercept) 0.0033881 0.05821 
 Residual              0.0099813 0.09991 
 Number of obs: 866, groups:  
   Line:Year, 548; Line:Loc, 532; Line, 195; Year, 3; Loc, 3
 
 Fixed effects:
   Estimate Std. Error t value
 (Intercept)   0.2365     0.0369    6.41


 biomass.blup = ranef(biomass.model)$Line
 write.table(biomass.blup,"Tuber-weight-from_per.plant_data3_195.lines.blup.csv",quote=F,sep=",")
 
 mm = as.data.frame(tapply(tuber.weight_multi$tuber.weight, tuber.weight_multi$Line, na.rm=T, mean))
 names(mm) = "mean"
 pdf("lines195_3.data.blup_mean.pdf")
 plot(biomass.blup[,1],mm$mean,xlab="Blup",ylab="Mean")
 dev.off()

biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Env) + (1|Line:Loc) + (1|Line:Year),data=tuber.weight_multi)

biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Env),data=tuber.weight_multi)
biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Env) + (1|Line:Env),data=tuber.weight_multi)
str(tuber.weight_multi)
tuber.weight_multi$Env <- factor(tuber.weight_multi$Loc : tuber.weight_multi$Year)
biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Env) + (1|Line:Env),data=tuber.weight_multi)



biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Loc:Year) + (1|Line:Loc:Year),data=tuber.weight_multi)
str(tuber.weight_multi)
tuber.weight_multi$Env <- tuber.weight_multi$Loc : tuber.weight_multi$Year
biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Env) + (1|Line:Env),data=tuber.weight_multi)
tuber.weight_multi$Env <- factor(tuber.weight_multi$Loc : tuber.weight_multi$Year)
biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Env) + (1|Line:Env),data=tuber.weight_multi)
table(tuber.weight_multi$Env)
biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Year) + (1|Line:Loc) + (1|Line:Year),data=tuber.weight_multi)
biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Env),data=tuber.weight_multi)
biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Env) + (1|Line:Loc) + (1|Line:Year),data=tuber.weight_multi)
biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Env) + (1|Line:Loc), data=tuber.weight_multi)
biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Line:Loc), data=tuber.weight_multi)
biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Env),data=tuber.weight_multi)
biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Env),data=tuber.weight_multi)
biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Env) + (1|Line:Loc) + (1|Line:Year),data=tuber.weight_multi)
biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Year), data=tuber.weight_multi)
biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Year) + (1|Loc:Year), data=tuber.weight_multi)
biomass.model = lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Year), data=tuber.weight_multi)

re <- ranef(fit, condVar=TRUE)
u <- re$Line
pev <- attr(u, "postVar")[1,1,]
s2_u <- VarCorr(fit)$Line[1,1]
r <- 1-pev/s2_u

re <- ranef(fit_s, condVar=TRUE)
u <- re$Line
pev <- attr(u, "postVar")[1,1,]
s2_u <- VarCorr(fit_s)$Line[1,1]
r <- 1-pev/s2_u



fit = lmer(tuber.weight ~ (1|Line) + (1|Loc) + (1|Year) + (1|Line:Loc) + (1|Line:Year),data=tuber.weight_multi_230)
ranef(fit, postVar=TRUE)
u <- ranef(fit, condVar=TRUE)
str(u)
re <- u
u <- re$Line
pev <- attr(u, "postVar")[1,1,]


fit = lmer(tuber.weight ~ (1|Line) + (1|Env),data=tuber.weight_multi_230)
re <- ranef(fit, condVar=TRUE)
u <- re$Line
pev <- attr(u, "postVar")[1,1,]
varmat <- VarCorr(fit)
str(varmat)
varmat$Line
summary(fit)
s2_u <- VarCorr(fit)$Line
str(varmat$Line)
s2_u <- VarCorr(fit)$Line[1,1]
r <- 1-pev/s2_u
str(r)
mean(r)
summary(r)



fit = lmer(tuber.weight ~ (1|Line) + (1|Env),data=tuber.weight_multi_230)


table(na.omit(tuber.weight_multi_230)$Line)

tab = table(na.omit(tuber.weight_multi_230)$Line)
selected_lines <- names(tab)[tab == 5]
fit_s = lmer(tuber.weight ~ (1|Line) + (1|Env),data=tuber.weight_multi_230[tuber.weight_multi_230$Line %in% selected_lines,])
re <- ranef(fit_s, condVar=TRUE)
u <- re$Line
pev <- attr(u, "postVar")[1,1,]
s2_u <- VarCorr(fit_s)$Line[1,1]
r <- 1-pev/s2_u
r
summary(fit_s)


fit_s = lmer(tuber.weight ~ (1|Line) + Env,data=tuber.weight_multi_230[tuber.weight_multi_230$Line %in% selected_lines,])
summary(fit_s)
> re <- ranef(fit_s, condVar=TRUE)
> u <- re$Line
> pev <- attr(u, "postVar")[1,1,]
> s2_u <- VarCorr(fit_s)$Line[1,1]
> r <- 1-pev/s2_u
> r


tab <- with(na.omit(tuber.weight_multi_230), table(Line, Loc))
tab > 1

inLoc <- as.numeric(tab > 0)
inLoc <- tab > 0
sum(rowSums(inLoc) > 1)
u
str(u)
u <- c(u)
r
lr <- lm(u ~ 1, weights=r)
lr <- lm(u ~ PC, weights=r)
lr <- lm(u ~ 1, weights=r/(1-r))
```
