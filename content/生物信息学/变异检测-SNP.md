---
title: 变异检测之-bwa/gatk-SNP/Indel
subtitle:
date: 2023-07-22T11:32:59+08:00
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
  - 生物信息学
categories:
  - 生物信息学
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

# [变异命名详解](https://zhuanlan.zhihu.com/p/108263386)  
## 变异的检测(SNP/Indel)
### SNP/Indel的变异检测
{{< admonition type=abstract open=false title="Bwa-GATK general pipeline" >}}
```
ref=*.fa #参考基因组的fa文件
reads1=R1.clean.fastq.gz reads2=R2.clean.fastq.gz #下机的二代双端数据
#Step1: Index 对参考基因组建立索引
bwa index -a is ${ref} #
#Step2: mem alignment 双端比对到参考基因组
bwa mem -t 10 -R "@RG\tID:test\tSM:test\tLB:test\tPL:ILLUMINA" ${ref} ${reads1} ${reads2} > test.sam 
#Step3: Sam2bam 比对后生成的sam文件转二进制的bam文件并排序
samtools view -bS test.sam -o test.bam 
samtools sort test.bam -o test.sort.bam
#Step4: 对reads进行prc重复的标记
picard MarkDuplicates REMOVE_DUPLICATES=false MAX_FILE_HANDLES_FOR_READ_ENDS_MAP=8000 INPUT=test.sort.bam OUTPUT=test.clean.marked.bam METRICS_FILE=test_clean.marked.bam.metrics
#Step5: bam文件建立索引文件
samtools index test.clean.marked.bam
#Step6: 变异检测之g.vcf文件的生成
gatk --java-options -Xmx8G HaplotypeCaller -R ${ref} -I test.clean.marked.bam -O test_clean.g.vcf.gz  -ERC GVCF
#Step7: 样本的合并生成群体变异数据
gatk --java-options Xmx256G CombineGVCFs -R ${ref} -V test_clean.g.vcf.gz -V test1_clean.g.vcf.gz -O All_samples.g.vcf.gz
#Step8: g.vcf文件转成常规vcf文件
gatk --java-options -Xmx256G GenotypeGVCFs -R ${ref} -V test_clean.g.vcf.gz -O test.vcf.gz
#Step9: 选择变异类型
gatk --java-options -Xmx256G SelectVariants -R ${ref} -O test_SNPs.vcf --variant test.vcf.gz --select-type-to-include SNP
#Step10: 基于硬过滤标准对SNP进行标记
#        各项指标QD/QUAL/SOR/FS/MQ/MQRankSum/ReadPosRankSum
gatk VariantFiltration -V test_SNPs.vcf  -filter "QD < 2.0" --filter-name "QD2" -filter "QUAL < 30.0" --filter-name "QUAL30" -filter "SOR > 4.0" --filter-name "SOR4" -filter "FS > 60.0" --filter-name "FS60" -filter "MQ < 40.0" --filter-name "MQ40" -filter "MQRankSum < -12.5" --filter-name "MQRankSum-12.5" -filter "ReadPosRankSum < -8.0" --filter-name "ReadPosRankSum-8" -O test_SNPs_filter.vcf
#Step11: 去掉不符合上步标准的变异
cat test_SNPs_filter.vcf | perl -ne 'print if /^#/ or /PASS/' > test_SNPs.final.vcf.gz
```
{{< /admonition >}}
### DBImport/CombineGVCF
{{< admonition type=abstract open=false title="DBImport/CombineGVCF" >}}
```
echo "what you need are these: file:intervals.list sample.list dir:Ref"
ref=./Ref/Melon_v4.0_PacBio.fasta

function form_map()
{
python pre.py sample.list #1175 reseq path
path=`pwd`"/gvcf"
for x in `cat  sample.list` ;do
echo -e "${x}\t${path}/${x}.g.vcf.gz" >> sample.map
done
}

function DBImport_01(){
if [ ! -d Chr ] ; then mkdir Chr ; else echo  "Directory <Chr> Exists" ;fi
for x in `cat intervals.list`;do
wd=`echo ${x} |awk -F : '{print $1}'`
echo "gatk --java-options -Xmx100G GenomicsDBImport --genomicsdb-workspace-path ./Chr/${wd} -L ${x} --sample-name-map sample.map" >> ${wd}.sh
echo "gatk --java-options -Xmx100G GenotypeGVCFs -R ${ref} -V gendb://./Chr/${wd} -O ./Chr/${wd}.vcf.gz" >> ${wd}.sh
echo "gatk --java-options -Xmx100G SelectVariants -R ${ref} -V ./Chr/${wd}.vcf.gz -O ./Chr/${wd}_snp.vcf.gz --select-type-to-include SNP" >> ${wd}.sh
echo "gatk --java-options -Xmx100G VariantFiltration  -filter \"QD < 2.0 || SOR > 4.0 || FS > 60.0 || MQ < 40.0 || MQRankSum < -12.5 || ReadPosRankSum < -8.0\" --filter-name \"Filter\" --cluster-window-size 5 --cluster-size 2 --missing-values-evaluate-as-failing -V ./Chr/${wd}_snp.vcf.gz -O ./Chr/${wd}_snp_mark.vcf.gz " >>${wd}.sh
echo "zcat ./Chr/${wd}_snp_mark.vcf.gz | perl -ne 'print if /^#/ or /PASS/' > ./Chr/${wd}_snp_final.vcf" >> ${wd}.sh
quick_qsub =1= {-q cu -l nodes=1:ppn=5} "bash ${wd}.sh 1>${wd}.log 2>${wd}.err" ##
done
}

function DBImport_02(){
echo "gatk --java-options -Xmx100G GatherVcfs \\" >> gather.sh
for x in `cat intervals.list`;do
wd=`echo ${x} |awk -F : '{print $1}'`
echo "-I ./Chr/${wd}_snp_final.vcf \\" >> gather.sh
done
echo "-O snp.vcf" >> gather.sh
quick_qsub =1= {-q cu -l nodes=1:ppn=5} "bash gather.sh 1 > log.gather 2 > err.gather"
}

function CombineGVCF(){
#echo "gatk CombineGVCFs -R ${ref} \\" >> Combine.sh
#cat ./sample.map|while read i;
#do
#sample=`echo ${i}|cut -f 2 -d ' '`
#echo "-V ${sample} \\" >> Combine.sh
#done
#echo "-O Raw.gvcf " >> Combine.sh
#echo "gatk --java-options -Xmx10G  GenotypeGVCFs -R ${ref}  -V Raw.gvcf -O Raw.vcf" >> Combine.sh
#echo "gatk --java-options -Xmx100G SelectVariants -R ${ref} -V Raw.vcf -O Raw_snp.vcf --select-type-to-include SNP" >> Combine.sh
echo "gatk --java-options -Xmx10g VariantFiltration -R ${ref} -V Raw_snp.vcf -O snp.vcf --filter-expression \"(QD < 2.0) || (FS > 60.0) || (MQ < 40.0) || (MQRankSum < -12.5) || (ReadPosRankSum < -8.0)\" --filter-name \"HF\" " >> Combine.sh
#echo "gatk --java-options -Xmx10g VariantFiltration -R ${ref} -V Raw_snp.vcf -O snp.vcf --filter-expression \"(QD < 2.0) || (FS > 60.0) || (MQ < 40.0) || (MQRankSum < -12.5) || (ReadPosRankSum < -8.0) ||(SOR > 4.0)\" --filter-name \"HF\" --cluster-window-size 5 --cluster-size 2 --missing-values-evaluate-as-failing" >> Combine.sh
echo "cat ./snp.vcf | perl -ne 'print if /^#/ or /PASS/' > ./Raw_snp_final.vcf" >> Combine.sh
quick_qsub =1= {-q cu -l nodes=1:ppn=5} "bash Combine.sh 1>log 2>err"
}

#form_map
#DBImport_01
#DBImport_02 #vast samples
CombineGVCF #a little samples

```
{{< /admonition >}}
### SNP提取特定位点的python脚本
1. py脚本可转pyc增加脚本性能
{{< admonition type=abstract title="py2pyc" open=false >}}
```
python -m compileall $1
mv __pycache__/* $1c
rm -d __pycache__
chmod +x $1c
```
{{< /admonition >}}

2. Extract.py
- 1. Extract.py file1.vcf file2.vcf
- 2. Extract.py file1.vcf file2.pos  
pos文件格式：‘染色体:物理位置’
{{< admonition type=abstract title="py script" open=false >}}
```
#!/home/yuqing/bin/python
#site_file type : *.pos *.vcf *.plink.vcf
#vcf_file type : *.vcf *.vcf.gz
import sys,gzip,os
if "gz" in sys.argv[1]:
  vcf_file=gzip.open(sys.argv[1], 'rt', encoding='utf-8')
elif "gz" not in sys.argv[1]:
  vcf_file=open(sys.argv[1],'r')
site_file=open(sys.argv[2],'r')
out_file=open("out.vcf",'w')
site_dic={}
num_f2 = 0
for l in site_file:
  if "pos" in sys.argv[2]:
    num_f2 += 1
    l=l.strip().split()
    site_dic[l[0]]=l[0]
  elif "vcf" in sys.argv[2]:
    if "#" in l:
      #out_file.write(l)
      pass
    elif "#" not in l:
      num_f2 += 1
      l=l.strip().split()
      if "chr0" in l[0]:
        site=f"{l[0][4:]}:{l[1]}"
      elif "chr1" in l[0]:
        site=f"{l[0][3:]}:{l[1]}"
      elif "chr" not in l[0]:
        site=f"{l[0]}:{l[1]}"
      site_dic[site] = '\t'.join(l)
site_file.close()
num_total,num_extract,num_exclude = 0, 0, 0
for l in vcf_file:
  if "#" in l:
    out_file.write(l)
    pass
  elif "#" not in l:
    num_total+=1
    l=l.strip().split()
    if "chr0" in l[0]:
      ch=l[0][4:]
    elif "chr1" in l[0]:
      ch=l[0][3:]
    elif "chr" not in l[0]:
      ch=l[0]
    k=f"{ch}:{l[1]}"
    try:
      try_flag=site_dic[k]
      del site_dic[k]
      num_extract += 1
      print(f"{l[2]}\t{ch}\t{l[1]}\t{l[3]}\t{l[4]}\t0")
      output='\t'.join(l)
      out_file.write(f"{output}\n")
    except Exception as e:
      num_exclude += 1
      print(f"{l[2]}\t{ch}\t{l[1]}\t{l[3]}\t{l[4]}\t1") #file 1
print(f"File1_Total:{num_total}\tExtract:{num_extract}\tExclude:{num_exclude}\nFile2_Total:{num_f2}")
for x in site_dic.keys():
  print(x)
vcf_file.close()
out_file.close()  
```
{{< /admonition >}}

### 将原始的vcf数据转成只有基因型的数据
- raw2info.py 
{{< admonition type=abstract title="py script" open=false >}}
```
#!/home/yuqing/bin/python
import sys
vcf=open(sys.argv[1],'r')
for x in vcf:
  if '##' in x:
    print(x.strip())
  elif '#CHROM' in x:
    print(x.strip())
  elif 'chr00' in x: #exclude chr00#lose
    pass
  elif '#' not in x:
    x=x.strip().split()
    if len(x[3].split(","))==1 and len(x[4].split(","))==1: #biallelic sites#lose
      gt,num="",0
      for z in x[9:]:
        num+=1
        if num != len(x[9:]):
          z=z.split(":")
          try:
            gt += f"{z[0]}\t"
            #gt += f"{z[0]}:{z[1]}:{z[3]}\t"
          except Exception as e:
            gt += f"{z[0]}\t"
            #gt += f"{z[0]}:{z[1]}:0\t"
        elif num == len(x[9:]):
          z=z.split(":")
          try:
            gt += f"{z[0]}"
            #gt += f"{z[0]}:{z[1]}:{z[3]}"
          except Exception as e:
            gt += f"{z[0]}"
            #gt += f"{z[0]}:{z[1]}:0"
      gt=gt.replace("|","/")
      #pri=f"{x[0]}\t{x[1]}\t.\t{x[3]}\t{x[4]}\t{x[5]}\t.\t.\tGT:AD:GQ\t{gt}"
      pri=f"{x[0]}\t{x[1]}\t.\t{x[3]}\t{x[4]}\t{x[5]}\t.\t.\tGT\t{gt}"
      print(pri)
vcf.close()
```
{{< /admonition >}}

### 对原始vcf数据进行SNP的过滤或质控
- filtration4vcf.py MAF Missing Het 
{{< admonition type=abstract title="py script" open=false >}}
```
#!/home/yuqing/bin/python
######Author:YuQing##########
######2022_10_11#########
import sys,os
os.system(f"date")
vcf=sys.argv[1] #plink_format
maf,miss,het = float(sys.argv[2]),float(sys.argv[3]),float(sys.argv[4])
if 'vcf' in vcf:
  os.system(f"echo -e 'Author: YQ\n2022_10_11\nFiltering based on the (Maf Miss Heterozygosity)'")
  os.system(f"echo Input vcf file firstly")
else:
  os.system(f"echo Input VCF")
  exit()
with open(vcf,'r') as vcf_file:
  head=vcf.split('.')[0]
  with open(f"filtered.vcf",'w') as vcf_filtration:
    dic, total_count,kept_count,maf_count, miss_count, het_count, three_count  = {}, 0, 0, 0, 0,0,0
    for l in vcf_file:
      if '#' in l:
        vcf_filtration.write(f"{l}")  
      elif 'GT' in l:
        total_count += 1
        l0=l.strip().split()
        ch,pos,g=l0[0],l0[1],l0[9:]
        if len(l0[3]) != 1 or len(l0[4]) != 1:
          three_count += 1
          continue
        rr_c,h_c,aa_c,mm_c,t_c = 0,0,0,0,0
        for g_s in g:
          t_c += 1
          if g_s.startswith("0/0",0,3) or g_s.startswith("0|0",0,3):
            rr_c += 1
          elif g_s.startswith("1/1",0,3) or g_s.startswith("1|1",0,3):
            aa_c += 1
          elif g_s.startswith("0/1",0,3) or g_s.startswith("0|1",0,3):
            h_c += 1
          elif g_s.startswith("./.",0,3) or g_s.startswith(".|.",0,3) or g_s.startswith(".",0,1): 
            mm_c += 1
        snp_rr,snp_h,snp_aa,snp_mm = rr_c/t_c, h_c/t_c, aa_c/t_c, mm_c/t_c
        snp_h = h_c/(t_c-mm_c)
        snp_r,snp_a = (2*rr_c+h_c)/(2*(t_c-mm_c)), (2*aa_c+h_c)/(2*(t_c-mm_c))
        if snp_r > snp_a:
          Maf = snp_a
        elif snp_r <= snp_a:
          Maf = snp_r
        if snp_mm >= miss:
          miss_count += 1
        elif Maf < maf:
          maf_count += 1  
        elif snp_h >= het:
          het_count += 1
        else:
          kept_count +=1
          vcf_filtration.write(f"{l}")
print(f"Total: {total_count}\nNot Biallelic: {three_count}\nMaf: {maf_count}\nMiss: {miss_count}\nHet: {het_count}\nKeep: {kept_count}")
os.system(f"date")
```
{{< /admonition >}}
- usage  
`python filtration4vcf.pyc $1.vcf 0.05 0.1 0.1 `
- 每个SNP的测序平均深度
{{< admonition type=abstract title="script" open=false >}}
```
vcftools --vcf $1.vcf --site-mean-depth  --out $1.mdp
cat $1.mdp.ldepth.mean|awk '{if($3>=5&&$3<=200)print$1":"$2}'|sed '1,$s/chr0//g'|sed '1,$s/chr//g' > $1.mdp.ldepth.mean.kept.pos
```
{{< /admonition >}}

## 变异文件分析
### vcftools变异质控
1. 次等位基因频率、缺失率、二等位基因型的质控  
` vcftools --vcf .vcf --maf 0.05 --min-alleles 2 --max-alleles 2 --max-missing 0.5 --recode --recode-INFO-all --out .vcf`
2. 基于样本ID和SNP位点ID的过滤  
`vcftools --vcf *.vcf --keep 个体 --recode --recode-INFO-all --out `  
`vcftools --vcf *.vcf --snps 位点 --recode --recode-INFO-all --out`
3. 统计SNP位点平均测序深度  
`vcftools --vcf $1 --site-mean-depth  --out $1_meandepth`
4. 变异位点转012格式  
`vcftools --vcf $1.vcf --012`
### plink变异质控
1. 次等位基因频率、缺失率  
`plink --vcf $1 --make-bed  -geno 0.1 -maf 0.05 --out $1`
2. 杂合率的统计  
```sh
plink --bfile $1 --hardy --out $1
paste <(cat $1.bim|awk '{print$1":"$4}') <(cat $1.hwe|grep -v CHR|awk '{print$7}') > $1.pos.het
cat $1.pos.het |awk '{if($2<0.1) print$1}' > $1.kept.pos #杂合率小于0.1
```
3. 基于样本ID和SNP位点ID的过滤  
`plink --vcf $1 --make-bed --remove-fam rmind.txt --out $1`  
`plink --vcf $1 --make-bed --keep keepind.txt --out $1`  
`plint --vcf $1 --make-bed --extract snp.keep --out $1`  
4. 维持参考和突变碱基  
`plink --vcf $1 --make-bed --real-ref-alleles --out $1`
5. 变异位点的连锁r2计算  
```sh
plink --bfile ${file} --ld-snp ${pos} --ld-window-kb 10000 --ld-window 999999 --ld-window-r2 0 --r2 --out check

```
### bcftools
1. 变异提取  
`bcftools filter ${input.vcf.gz} --regions 01:1000-2000 > GeneX.vcf`

### In-House Script
1. 提取变异位点  
`python ExtractSite.pyc $1.vcf $1.kept.pos ; mv out.vcf $1.filters.plink.vcf`  
```python
#!/home/yuqing/bin/python
#site_file type : *.pos *.vcf *.plink.vcf
#vcf_file type : *.vcf *.vcf.gz
import sys,gzip,os
if "gz" in sys.argv[1]:
	vcf_file=gzip.open(sys.argv[1], 'rt', encoding='utf-8')
elif "gz" not in sys.argv[1]:
	vcf_file=open(sys.argv[1],'r')
site_file=open(sys.argv[2],'r')
out_file=open("out.vcf",'w')
site_dic={}
num_f2 = 0
for l in site_file:
	if "pos" in sys.argv[2]:
		num_f2 += 1
		l=l.strip().split()
		site_dic[l[0]]=l[0]
	elif "vcf" in sys.argv[2]:
		if "#" in l:
			#out_file.write(l)
			pass
		elif "#" not in l:
			num_f2 += 1
			l=l.strip().split()
			if "chr0" in l[0]:
				site=f"{l[0][4:]}:{l[1]}"
			elif "chr1" in l[0]:
				site=f"{l[0][3:]}:{l[1]}"
			elif "chr" not in l[0]:
				site=f"{l[0]}:{l[1]}"
			site_dic[site] = '\t'.join(l)
site_file.close()
num_total,num_extract,num_exclude = 0, 0, 0
for l in vcf_file:
	if "#" in l:
		out_file.write(l)
		pass
	elif "#" not in l:
		num_total+=1
		l=l.strip().split()
		if "chr0" in l[0]:
			ch=l[0][4:]
		elif "chr1" in l[0]:
			ch=l[0][3:]
		elif "chr" not in l[0]:
			ch=l[0]
		k=f"{ch}:{l[1]}"
		try:
			try_flag=site_dic[k]
			del site_dic[k]
			num_extract += 1
			print(f"{l[2]}\t{ch}\t{l[1]}\t{l[3]}\t{l[4]}\t0")
			output='\t'.join(l)
			out_file.write(f"{output}\n")
		except Exception as e:
			num_exclude += 1
			print(f"{l[2]}\t{ch}\t{l[1]}\t{l[3]}\t{l[4]}\t1") #file 1
print(f"File1_Total:{num_total}\tExtract:{num_extract}\tExclude:{num_exclude}\nFile2_Total:{num_f2}")
for x in site_dic.keys():
	print(x)
vcf_file.close()
out_file.close()	
```
2. 过滤变异位点
```python
#!/home/yuqing/bin/python
######Author:YuQing##########
######2022_10_11#########
import sys,os
os.system(f"date")
vcf=sys.argv[1] #plink_format
maf,miss,het = float(sys.argv[2]),float(sys.argv[3]),float(sys.argv[4])
if 'vcf' in vcf:
	os.system(f"echo -e 'Author: YQ\n2022_10_11\nFiltering based on the (Maf Miss Heterozygosity)'")
	os.system(f"echo Input vcf file firstly")
else:
	os.system(f"echo Input VCF")
	exit()
with open(vcf,'r') as vcf_file:
	head=vcf.split('.')[0]
	with open(f"{head}.filtered.vcf",'w') as vcf_filtration:
		dic, total_count,kept_count,maf_count, miss_count, het_count, three_count  = {}, 0, 0, 0, 0,0,0
		for l in vcf_file:
			if '#' in l:
				vcf_filtration.write(f"{l}")	
			elif 'GT' in l:
				total_count += 1
				l0=l.strip().split()
				ch,pos,g=l0[0],l0[1],l0[9:]
				if len(l0[3]) != 1 or len(l0[4]) != 1:
					three_count += 1
					continue
				rr_c,h_c,aa_c,mm_c,t_c = 0,0,0,0,0
				for g_s in g:
					t_c += 1
					if g_s.startswith("0/0",0,3) or g_s.startswith("0|0",0,3):
						rr_c += 1
					elif g_s.startswith("1/1",0,3) or g_s.startswith("1|1",0,3):
						aa_c += 1
					elif g_s.startswith("0/1",0,3) or g_s.startswith("0|1",0,3):
						h_c += 1
					elif g_s.startswith("./.",0,3) or g_s.startswith(".|.",0,3) or g_s.startswith(".",0,1):	
						mm_c += 1
				snp_rr,snp_h,snp_aa,snp_mm = rr_c/t_c, h_c/t_c, aa_c/t_c, mm_c/t_c
				snp_h = h_c/(t_c-mm_c)
				snp_r,snp_a = (2*rr_c+h_c)/(2*(t_c-mm_c)), (2*aa_c+h_c)/(2*(t_c-mm_c))
				if snp_r > snp_a:
					Maf = snp_a
				elif snp_r <= snp_a:
					Maf = snp_r
				if snp_mm >= miss:
					miss_count += 1
				elif Maf < maf:
					maf_count += 1	
				elif snp_h >= het:
					het_count += 1
				else:
					kept_count +=1
					vcf_filtration.write(f"{l}")
print(f"Total: {total_count}\nNot Biallelic: {three_count}\nMaf: {maf_count}\nMiss: {miss_count}\nHet: {het_count}\nKeep: {kept_count}")
os.system(f"date")
```
