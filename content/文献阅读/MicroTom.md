---
title: MicroTom
subtitle:
date: 2024-09-21T21:01:53+08:00
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
  - 文献阅读
categories:
  - 文献阅读
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
题目：[MicroTom Metabolic Network: Rewiring Tomato Metabolic Regulatory Network throughout the Growth Cycle](https://www.sciencedirect.com/science/article/pii/S1674205220301830)  
文章单位：四川大学  
通讯作者：[张阳](https://life.scu.edu.cn/info/1121/4638.htm)  
- [Abstract](#Abstract)
- [Introduction](#Introduction)
- [Result](#Result)
- [Method](#Method)
- [Fig](#Fig)
## Abstract {#Abstract}
- Tomato (Solanum lycopersicum) is a major horticultural crop worldwide and has emerged as a preeminent(卓越的) model for metabolic research.
- Although many research efforts have focused on the analysis of metabolite differences between varieties and species, the dynamics of metabolic changes during the tomato growth cycle and the regulatory networks that underlie these changes are poorly understood.
- In this study, we integrated high-resolution spatio-temporal metabolome and transcriptome data to systematically explore the metabolic landscape across 20 major tomato tissues and growth stages.
- In the resulting MicroTom Metabolic Network, the 540 detected metabolites and their co-expressed genes could be divided into 10 distinct clusters based on their biological functions.
- Using this dataset, we constructed a global map of the major metabolic changes that occur throughout the tomato growth cycle and dissected the underlying regulatory network.
- In addition to verifying previously well-established regulatory networks for important metabolites,we identified novel transcription factors that regulate the biosynthesis of important secondary metabolites such as steroidal glycoalkaloids and flavonoids(甾族糖苷生物碱和类黄酮).
- Our findings provide insights into spatiotemporal changes in tomato metabolism and generate a valuable resource for the study of metabolic regulatory processes in model plants.
## Introduction {#Introduction}
## Result {#Result}
### <font color="#4169E1">Generation of the MMN Dataset</font>
>- To create a comprehensive and accurate record of changes to metabolic regulatory networks during the life cycle ofMicroTomtomato, we generated the MMN dataset (Figure 1).
- This dataset consists of parallel metabolic profiling and transcriptome analysis for samples collected from all major growth stages and tissues of MicroTom tomato.
- We collected 20 tissues: roots, stems, and leaves from the bud stage (when the first flower bud emerges, 30 days post-germination [DPG]), the flowering stage (when 50% of flowers reach anthesis, 45 DPG), and the breaker stage (when the first fruit reaches the breaker stage, 85 DPG).
- Bud and flower samples were collected from bud-stage seedlings and flowering-stage seedlings, respectively.
- In addition, we collected pericarps at nine stages of fruit development (10 days post-anthesis [DPA], 20 DPA, immature green, mature green [MG], breaker [Br], 3 days post breaker stage [Br3], Br7, Br10, and Br15) (Figure 1).
- Three biological replicates, each of which was a pooled sample from ten plants, were analyzed for all 20 time points/tissues.
>- For metabolome analysis, samples were analyzed using a broadly targeted LC-tandem MS (LC-MS/MS)-based metabolic profiling method (Zhu et al., 2018) (see Methods).
- A total of 540 distinct annotated metabolites were identified in at least one tissue, including 70 flavonoids, 76 amino acid and derivatives, 54 lipids, 52 organic acids, 50 nucleotide and derivatives, 14 phenolamides, 32 alkaloids, 43 hydroxycinnamoyl and derivatives, nine polyphenols, 13 carbohydrates, 12 vitamins, 10 benzoic acid and derivatives, 18 polyamines, and 87 additional compounds that did not fit into these 13 main classes (Figure 2A and Supplemental Data 1).
- Analysis of the 540 metabolites among different tissues showed that they could be divided into three large groups: metabolites present in vegetative tissues (roots, stems, and leaves), flower tissues (buds and flowers), and fruit tissues (pericarp throughout fruit development) (Figure 2A).
- This result indicates that vegetative tissues at different developmental stages have similar metabolic patterns, which are significantly different from those of fruit tissues.
- For example, metabolites such as lipids, alkaloids, hydroxycinnamoyl and derivatives, and phenolamides accumulate preferentially during vegetative tissues, whereas fruit tissues have substantially higher levels of amino acid and their derivatives, flavonoids, nucleotide and their derivatives, organic acids, polyphenols, and vitamins (Figure 2A).
- These specific metabolites likely reflect the spatial differentiation of tomato metabolism between the two major phases: vegetative growth and fruit development.
- In addition, we performed principal component analysis (PCA) and established that the 540 metabolites could be further divided into five groups, each associated with a specific tissue (roots, stems, leaves, flowers, and fruit) (Figure 2C).
- In line with the PCA, the cluster dendrogram could also be divided into five independent subgroups (Figure 2E).
- Taken together, these data indicate that the accumulation of metabolites during tomato development is tissue specific.
>- To investigate transcriptional regulation over the course of the MicroTom tomato growth cycle, we built a spatio-temporal dynamic transcriptome landscape for all tissues.
- Approximately 453 Gb of raw data were generated, and the statistics of the sequencing libraries are summarized in Supplemental Data 2.
- Unique mapped reads were used to calculate expression levels in transcripts per million (TPM) (Bo et al., 2010; Wagner et al., 2012).
- To reduce the influence of transcriptional noise, we defined a gene as expressed if its average TPM value was >0.
- In total, 31 256 genes were found to be expressed in at least one sample (Supplemental Data 3).
- To draw a global picture of gene expression across the 20 tissues, we made a Z-score normalized expression heatmap clustered by genes.
- A correlation matrix of the transcriptome indicated that the global gene expression pattern was tissue-specific, regardless of developmental stage (Figure 2B and Supplemental Data 3).
- As those established for the metabolome, the PCA and the cluster dendrogram of the transcriptome also showed clustering of samples from the same tissues among different stages (Figure 2D and 2F).
- All these results suggest that gene expression and metabolite accumulation show significant tissue specificity during tomato development.
### <font color="#4169E1">The Tomato Metabolome and Transcriptome Are Coregulated in ten Clusters That Correspond to Different Tissues and Developmental Stage</font>
>- To gain further insight into metabolic changes during the Micro- Tom growth cycle, we divided all 540 annotated metabolites into ten clusters based on their accumulation patterns using the k-means clustering algorithm (Howe et al., 2010) (Supplemental Figure 1A, Table 1, Supplemental Data 4).
- By analyzing the ten clusters, we identified metabolites that were enriched in specific tissues, such as roots (cluster I), stems (cluster III), leaves (cluster IV), and flowers (cluster V) (Figure 3 and Supplemental Figure 1A).
- We also identified compounds whose contents decreased during the period between the flowering and ripe fruit stages (cluster VI) and compounds whose levels increased during the green fruit stages (cluster VII) and during the fruit-ripening stages (cluster X).
- In addition, some compounds were enriched in more than two tissues or stages (clusters II, VIII, and IX) (Figure 3 and Supplemental Figure 1A).
>- To further correlate gene expression patterns with metabolite accumulation, we applied co-expression analysis to our metabolome and transcriptome data (Serin et al., 2016; Giovannoni, 2018).
- A rigorous multiple test correction (r R 0.8) was used to filter the genes that were significantly correlated with each metabolite.
- A total of 17 003 genes that were co-regulated with at least one metabolite were identified (Supplemental Figure 1B, Supplemental Data 4 and 5).
>- Next, the 540 metabolites and 17 003 genes were divided into ten co-expression clusters based on the Pearson correlation coefficient, and they exhibited a consistent and clear expression pattern during tomato development (Figure 3).
- Interestingly, after removing genes that were not highly correlated with any of the 540 metabolites, the PCA (Supplemental Figure 2A) and clustering analysis (Supplemental Figure 2B) of the remaining 17 003 highly co-expressed genes still showed clustering patterns similar to the global gene expression clusters (Supplemental Figure 1B).
- This indicates that during the normal growth cycle, the pattern of tomato gene expression is largely paralleled by the dynamics of major metabolic pathways..

### <font color="#4169E1">Insights into the Spatio-temporal Regulation of Key Metabolic Pathways</font>
- To examine whether the MMN could provide insights into the spatio-temporal metabolic regulatory network in tomato, we first tested it with previously known regulatory networks.
- Flavonoid biosynthesis branches from the phenylpropanoid pathway, which provides precursors in the form of phenylalanine.
- After the reactions catalyzed by the gateway enzymes phenylalanine ammonia lyase and chalcone synthase, the flavonoid pathway consists of a series of enzymes that catalyze diverse downstream reactions, leading to the biosynthesis of aglycone backbones (Figure 4D).
- Flavonoid biosynthesis has attracted increasing research attention over the past two decades, and much progress has been made in the identification of both the biosynthetic genes and their regulators (Vogt, 2010).
- Multiple MYB family transcription factors have been identified as regulatory factors in flavonoid biosynthesis (Borevitz et al., 2000; Mehrtens et al., 2005; Ballester et al., 2010).
- It has been suggested that the expression of Flavonoid-30,50-hydroxylase (SlF3050H), a flavonoid modification gene, is correlated with the anthocyanin biosynthetic transcription factor SlMYB75 in vegetative tissues, rather than with SlMYB12, the predominant regulator of flavonoid biosynthesis (Ballester et al., 2010; Jian et al., 2019).
- SlF3050H expression is also crucial for the activation of anthocyanin synthesis in tomato fruit because tomato dihydroflavonol 4-reductase prefers dihydromyricetin (three –OHs on the B ring) over dihydrokaempferol (one –OH on the B ring) (Silvia et al., 2009).
- In line with previous results, our RNA-seq data for flavonoid biosynthetic genes and associated transcription factors revealed that SlF3050H was strongly co-expressed with SlMYB75 but not with SlMYB12 (Figure 4A and 4B).
- A quantitative real-time PCR (qRT–PCR) analysis of these genes produced results that were highly consistent with the RNAseq data (Supplemental Figure 3, Supplemental Data 6).
- A dual luciferase reporter assay revealed that SlMYB75 interacted with the promoter region of SlF3050H to induce much higher expression than that induced by SlMYB12 (Figure 4C).
- In summary, our spatio-temporal data show good correlation between metabolite production and transcriptome changes, suggesting that the MMN can be used to study the regulation of important metabolic pathways in tomato.
- SGA biosynthesis begins with glycolysis, followed by the mevalonate and cycloartenol pathways.
- The cholesterol pathway generates cholesterol, a precursor of the SGA pathway, and the phytosterol pathway overlaps with the cholesterol pathway (Sonawane et al., 2016) (Supplemental Figures 4A and 5).
- From cholesterol, a series of enzymes catalyzes diverse downstream reactions in the pathway leading to the biosynthesis of SGAs (Supplemental Figure 4A).
- Previous co-expression analyses identified clustered GLYCOALKALOID METABOLISM (GAME) genes that form the biosynthetic pathway from cholesterol to a-tomatine (Itkin et al., 2013).
- In addition, SlGAME9, an APETALA2/ethylene response factor (AP2/ERF) transcription factor, was found to positively regulate SGA biosynthesis (Ca´ rdenas et al., 2016).
- Among the 540 metabolites, we detected 29 SGAs that were mainly present in clusters III, V, VI, and X (Supplemental Data 7).
- Interestingly, we identified three SGAs (dehydrofilotomatine, dehydrotomatine, and dehydrotomatine isomer (25R)) and 15 SGA-related genes in cluster V (Supplemental Figures 4 and 6A).
- Among these, the SGA biosynthetic genes (SlGAME1, SlGAME4, SlGAME6, SlGAME11, SlGAME17, and SlGAME25) co-expressed well with the regulatory gene SlGAME9 (Supplemental Figure 6B).
- This result is consistent with previous co-expression analysis of the GAME gene cluster (Itkin et al., 2013; Ca´ rdenas et al., 2016).
- We also performed qRT–PCR analysis of these genes and found that their expression was increased in vegetative tissues and decreased during fruit development (Supplemental Figure 7).
- In summary, we can use the MMN to accurately verify previously known metabolic regulatory networks throughout the tomato growth cycle..
### <font color="#4169E1">Identification of a Novel Transcription Factor That Regulates Steroidal Glycoalkaloid Metabolism</font>
- We next attempted to use the MMN to identify new regulators that control the SGA biosynthetic pathway, given that these defense compounds are also important for tomato growth and fruit quality (Itkin et al., 2013; Zhu et al., 2018).
- Our clustering data indicated that 15 SGA-related genes (SlGAME9 and 14 biosynthetic genes) were co-expressed with three SGAs in cluster V.
- We searched this cluster and found that a gene (Solyc01g096370) encoding a basic-helix-loop-helix (bHLH) transcription factor was also strongly co-expressed with these SGAs and metabolic genes (Figure 5A).
- Further investigation indicated that Solyc01g096370 shared a large number of co-regulated metabolites and genes with the known regulator SlGAME9 (Ca´ rdenas et al., 2016) (Supplemental Figure 8A).
- Kyoto Encyclopedia of Genes and Genomes (KEGG) analysis of the common genes and metabolites revealed that their molecular functions were primarily enriched in steroid and alkaloid biosynthesis, which suggested that Solyc01g096370 could potentially modulate the SGA pathway (Supplemental Figure 8B).
- Intriguingly, the level of correlation between Solyc01g096370 and the SGA pathway was as good as that of SlGAME9 (Figure 5A).
- Phylogenetic analysis revealed that the bHLH family protein encoded by Solyc01g096370 belonged to the MYC family (Supplemental Figure 9A and 9B), which is mainly involved in jasmonate (JA) signaling (Deng et al., 2015; Chen et al., 2016; Du et al., 2017, 2018).
- Further analysis indicated that Solyc01g096370 is SlbHLH114, which belongs to bHLH subfamily 15 (Supplemental Figure 9C) (Hua et al., 2015) and is related to JA signaling and the development of type VI glandular trichomes in S.
- lycopersicum (Kemparaju, 2018).
- Moreover, SlbHLH114 was clustered with subfamily 8 from Arabidopsis thaliana (Supplemental Figure 9D), which functions in JA signal transduction pathways and affects the formation of root hairs and trichomes (Tominaga-Wada et al., 2011).
- These data suggest that SlbHLH114 may be involved in SGA metabolism and JA signaling.
- We then analyzed the expression levels of SlbHLH114 at different developmental stages and in different tissues.
- Our transcriptome analysis indicated that expression of SlbHLH114, like that of known SGA biosynthetic genes and metabolites, was high in vegetative tissues and gradually decreased during fruit development to a very low level at fruit-ripening stages (Supplemental Figures 4B and 9E).
- qRT–PCR analysis confirmed this expression pattern (Supplemental Figure 9F).
- Subcellular localization showed that SlbHLH114 was exclusively located in the nucleus (Supplemental Figure 10).
- To investigate the potential function of SlbHLH114, we generated transgenic tomato plants overexpressing SlbHLH114 driven by the fruit specific E8 promoter.
- We obtained 17 T0 plants in which the expression levels of SlbHLH114 in ripening-stage fruit were significantly higher than those of MicroTom (Supplemental Figure 11).
- Two of these lines (line C and line I) were chosen for further characterization of the T1 generation (Figure 5B and 5D).
- We performed RNA-seq analysis of Br3-stage pericarp samples from wild-type (WT) and T1 generation E8:bHLH114 line C and line I plants (Figure 5B).
- A large proportion of the induced genes were shared by E8:bHLH114 line C and line I, including many genes and metabolites in the SGA biosynthetic pathway (Figure 5C).
- Compared with MicroTom tomato fruit at the same stage, both E8:bHLH114- overexpressing lines had 2851 upregulated genes and 2153 downregulated genes (FC R 1.5) (Supplemental Figure 12A, Supplemental Data 8 and 9).
- KEGG enrichment analysis indicated that the upregulated genes were involved in signal transduction, plant–pathogen interaction, and the biosynthesis of secondary metabolites related to SGAs (Supplemental Figure 12B, Supplemental Data 10).
- qRT–PCR analysis confirmed this observation; in general, genes involved in glycolysis and in the mevalonate, cycloartenol, cholesterol and SGA pathways were all upregulated in both E8:SlbHLH114 lines (Supplemental Figure 13).
- As a result, the metabolic profiling of pericarp samples at the Br10 stage showed that both transgenic lines accumulated significantly higher amounts of SGAs (predominantly tomatidine, hydroxytomatidenol, hydroxytomatidine, gtomatine, b2-tomatine, and a-tomatine) (Figure 5C).
- Taken collectively, these results indicate that the overexpression of SlbHLH114 in tomato fruit enhances SGA accumulation.
- To further investigate whether SlbHLH114 directly induces the expression of SGA biosynthetic genes, we performed dual luciferase reporter assays using Arabidopsis protoplasts.
- We cloned the promoters of three SlbHLH114-induced biosynthetic genes involved in the cholesterol precursor pathway (SlSSR2 and Sl7-DR2) and the SGA biosynthetic pathway (SlGAME4).
- With SlGAME9 as a positive control, the results showed that the activities of these promoters were all significantly higher when SlbHLH114 was expressed than in the control (Figure 5E and 5F), indicating that SlbHLH114 is a positive regulator of the SGA biosynthetic pathway.
- Previously, SlMYC2 (Solyc08g076930) was reported to be a key regulator of SGA biosynthesis (Ca´ rdenas et al., 2016).
- We conducted co-expression analysis of SlMYC2 and SGA-related genes and found that SlMYC2 did not co-express well with known SGA genes.
- Instead, it had strong correlations with JA-signaling genes, consistent with its important role in regulating JA signaling (Supplemental Figure 14) (Du et al., 2017; Liu et al., 2019).
- We then performed co-expression analysis of SlMYC2 and SlbHLH114 using our MMN dataset, as well as the previously published SGN-TEA (http://tea.solgenomics.net/overview) (Shinozaki et al., 2018) and TomExpress datasets (http:// tomexpress.toulouse.inra.fr/) (Zouine et al., 2017).
- In all three datasets, there was no significant co-expression between SlMYC2 and SlbHLH114 (Supplemental Figure 15).
- Both SlMYC2 and SlbHLH114 belong to bHLH subfamily 15 (Supplemental Figure 16) (Hua et al., 2015).
- To investigate the possible interaction between SlMYC2 and SlbHLH114, we conducted dual luciferase reporter assays in Arabidopsis protoplasts and found that probHLH114 could be activated by SlMYC2 (Supplemental Figure 17A), indicating that SlbHLH114 was a target of SlMYC2.
- On the other hand, we checked previously published SlMYC2-related work and found that SlbHLH114 expression in SlMYC2-RNAi plants was significantly lower than that in WT plants (Du et al., 2017), confirming SlMYC2 is a potential regulator of SlbHLH114 expression (Supplemental Figure 17B).
- By contrast, no significant induction of proSlMYC2 by SlbHLH114 was observed in the dual luciferase reporter assays (Supplemental Figure 17C).
- In addition, in our RNA-seq data from E8:bHLH114 and WT fruit, there were no significant differences in SlMYC2 expression levels (Supplemental Figure 17D).
- All these data indicate SlbHLH114 cannot directly regulate the expression of SlMYC2.
### <font color="#4169E1">Prediction and Verification of a Novel Transcription Factor That Regulates Flavonoid Metabolism</font>
- Using the same strategy described above, we used the MMN to expand our search for transcription factors that regulate flavonoid metabolism.
- Interestingly, when we conducted coexpression analysis of flavonoid compounds and biosynthetic genes, we found that in addition to the known gene SlMYB12, a gene (Solyc02g077790) that encoded an AP2/ERF transcription factor was co-expressed more strongly with the flavonoid metabolic pathway (Figure 6A).
- Further investigation showed that Solyc02g077790 shared a large number of co-expressed genes and metabolites with SlMYB12.
- KEGG analysis of the common genes and metabolites revealed that their molecular functions were mainly enriched in flavonoid and phenylpropanoid biosynthesis, suggesting that Solyc02g077790 could potentially modulate the flavonoid pathway (Supplemental Figure 18).
- Phylogenetic analysis of the AP2/ERF family in S.
- lycopersicum indicated that the Solyc02g077790 protein belonged to ERF subgroup G and could be designated SlERF.G3-like (Supplemental Figure 19A) (Liu et al., 2016).
- RNA-seq and qRT–PCR analyses both indicated that SlERF.G3-like was specifically expressed in fruit tissues and reached its highest expression level at Br3 (Supplemental Figure 19B), similar to the expression pattern of major flavonoid biosynthetic genes and metabolites.
- Subcellular localization further indicated that SlERF.G3-like localizes to the nucleus and the cytoplasm (Supplemental Figure 10).
- To investigate the function of SlERF.G3-like, we generated transgenic MicroTom plants overexpressing SlERF.G3-like under the fruit-specific E8 promoter.
- We obtained 14 independent E8:SlERF.G3-like overexpression lines, of which two representative lines (lines 12 and 36) were selected for further study (Figure 6B and 6C and Supplemental Figure 20).
- We then performed qRT–PCR analysis of SlERF.G3-Like-12, SlERF.G3- Like-36, and WT pericarp samples at the Br3 stage and found that the expression of flavonoid biosynthesis genes, including SlCHS1, SlCHS2, SlCHI, SlF3H, SlF30H, and SlFLS, was significantly increased in the two transgenic lines (Figure 6B and 6D).
- In line with the increased expression of biosynthetic genes, LC-MS analysis of Br7-stage fruits showed a significant increase in the contents of major flavonoid compounds and intermediates (naringenin, eriodictyol, kaempferol-3-O-glucoside, kaempferol-3-O-rutinoside, quercetin-3-O-glucoside, and quercetin-3-O-rutinoside) (Figure 6D).
- As both E8:SlERF.G3-like lines 12 and 36 showed an orange color (Figure 6B), we also measured the expression of carotenoid biosynthetic genes.
- Compared with MicroTom, there was no significant reduction in the expression of carotenoid biosynthesis genes in E8:SlERF.G3-like-36 fruits (Supplemental Figure 21).
- This matches our previous observation on flavonoidenriched tomato (Zhang et al., 2015a; Ying et al., 2020).
- All these data indicate that the orange color of E8:SlERF.G3-like fruit is mainly due to the accumulation of flavonoid compounds, rather than to the inhibition of carotenoid biosynthesis.
- To directly compare the functions of SlERF.G3-like with those of the known regulator of flavonoid biosynthesis, SlMYB12, we analyzed the promoters of major flavonol biosynthesis genes (SlCHS1, SlF3H, and SlFLS) by dual luciferase reporter assays in Arabidopsis protoplasts.
- The results showed that all three promoters were significantly induced by SlMYB12 and SlERF.G3- like (Supplemental Figure 22).
- In addition, when both transcription factors (TFs) were combined, the promoter activities were increased further (Supplemental Figure 22).
- However, because the expression levels of SlMYB12 did not differ significantly between E8:SlERF.G3-like and WT fruits (Supplemental Figure 23A), and the transcript abundance of SlERF.G3-like does not change in fruits overexpressing AtMYB12 (the A.
- thaliana homolog of SlMYB12) (Supplemental Figure 23B), we concluded that there is no direct interaction between SlMYB12 and SlERF.G3-like, although both TFs can upregulate flavonoid biosynthesis.
- In particular, we checked the expression of SlMYB12 and SlERF.G3-like in the peel and flesh of WT pericarp at Br3.
- Compared with SlMYB12, which is mainly expressed in the fruit peel (Adato et al., 2009), SlERF.G3-like was significantly induced in the flesh (Supplemental Figure 23C and 23D).
- Furthermore, low expression correlation between the two genes was observed in the MMN, SGN-TEA (Shinozaki et al., 2018), and TomExpress (Zouine et al., 2017) databases (Supplemental Figure 24).
- All these data suggest that the two TFs may act independently to regulate flavonol biosynthesis in tomato fruits.
- These results together indicate that SlERF.G3-like is a TF that may regulate flavonoid biosynthesis in tomato.
- Thus, the MMN dataset can help uncover the metabolic regulatory networks that operate during the tomato growth cycle and verify novel regulators of major metabolic pathways.

## Method {#Method}
### Plant Materials and Tissue Preparation 
- Tomato (S.lycopersicum cv MicroTom) seeds were obtained from PanAmerican Seed.
- MicroTom plants were grown in a climate-controlled growth room with a light/dark photoperiod of 16/8 h at 23C.
- Four- to 5- week-old plants with five to six expanded true leaves and one bud were used for the bud stage (30 DPG).
- Six- to 7-week-old plants with more than 50% flowers were used for the flowering stage (45 DPG).
- Twelveto 13-week-old plants with one breaker fruit were used for the breaker stage (85 DPG).
- Root, stem, and leaf tissues were collected at all three stages, and leaf tissue was collected from the fifth true leaf to all healthy young leaves.
- Flowers at anthesis (0 DPA) were tagged, and expanding fruits were harvested at 10, 20, and 30 DPA (immature green).
- Mature and ripening fruits were harvested based on the tomato color chart ‘‘USDA Visual Aid TM-L-1’’ (USDA, 1975) as follows: MG-stage (full-size green fruit, approximately 35 DPA), Br (Breaker)-stage (definite break in color from green to tannish-yellow on not more than 10% of the surface, approximately 40 DPA), and 3, 7, 10, and 15 days later (Br3, Br7, Br10, and Br15, respectively).
- All samples were collected before the greenhouse lights were turned off at approximately 7:00–9:00 p.m.
- Samples from ten individual plants were pooled as one biological replicate and immediately frozen in liquid nitrogen.
- Three biological replicates were used in later transcriptome and metabolome analysis.
### Generation of the MMN Dataset: Metabolome Profiling and Transcriptome Profiling 
- Metabolome profiling was carried out using a widely targeted metabolome method by Wuhan Metware Biotechnology Co., Ltd (Wuhan, China) (http://www.metware.cn/).
- In brief, the tomato tissues were lyophilized and ground into a fine powder using a mixer mill (MM 400, Retsch) with a zirconia bead for 1.5 min at 30 Hz.
- The tissue powder (100 mg) was weighed and extracted overnight with 1.0 mL 70% aqueous methanol at 4C, followed by centrifugation for 10 min at 10 000 g.
- All supernatants were collected and filtered using a membrane (SCAA-104, 0.22 mm pore size; ANPEL, Shanghai, China, http://www.anpel.com.cn/) before the LC-MS analysis.
- Quantification of metabolites was carried out using a scheduled multiple reaction monitoring method (Wei et al., 2013; Zhu et al., 2018).
- Transcriptome profiling was performed as described previously (Ying et al., 2020).
- In brief, clean reads obtained from the Hiseq X Ten sequencing platform were mapped to the tomato reference genome (version 3.0) (The Tomato Genome Consortium, 2012) using HISAT2 (Daehwan et al., 2015), then normalized to TPM using StringTie (Pertea et al., 2015).
- All raw data were deposited in the Genome Sequence Archive at the Big Data Center, Beijing Institute of Genomics, Chinese Academy of Sciences, under accession numbers CRA001723 and CRA001712 and are publicly accessible at http://bigd.big.ac.cn/gsa (Wang et al., 2017; Members, 2018).
### Co-expression/Co-regulation Cluster Identification and Analysis 
- Co-expression/co-regulation analysis was performed on samples from 20 different time points and tissues using MeV (version 4.9) with the k-means method (Gasch and Eisen, 2002).
- Normalized expression values of genes and metabolites were calculated by dividing their expression level at all samples with their maximum observed TPM.
- Hierarchical clustering (HCL) and PCA were performed using the prcomp function in R software with default settings (R Core Team, 2013) to facilitate graphical interpretation of the relatedness among samples from 20 different time points/tissues.
- The transformed and normalized gene and metabolite expression values with Z-scores were used for hierarchical clustering and PCA.
### Construction of a Gene and Metabolite Regulatory Network 
- We used the Pearson’s correlation algorithm method (Bishara and Hittner, 2012) to construct a TF-related gene and metabolite regulatory network.
- Mutual information for calculating the similarity in expression levels between pairs of TFs and genes/metabolites was calculated using R software.
- All associations among TFs and genes/metabolites were visualized using Cytoscape software (Kohl et al., 2011).
### Sequence Alignment and Phylogenetic Analyses 
- Sequence alignments were performed using the MUSCLE algorithm in MEGA7 (Edgar, 2004).
- Molecular phylogenetic analysis was performed using an NJ matrix-based model.
- Bootstrap values were calculated using 1000 replicates.
- All phylogenetic analyses were conducted in MEGA7.
### Sample Extraction and Metabolomic Analysis 
- Extract preparation and flavonoid profiling of tomato fruit tissues were performed as described previously (Ying et al., 2020).
- For the measurement of SGAs, tomatoes were harvested 10 days after the breaker stage (Br10).
- Fruit pericarp was freeze-dried and ground into a fine powder using an automatic sample rapid grinder (JXFSTPRP-24, Shanghai Jingxin Industrial Development Co., Ltd) three times for 1 min at 50 Hz.
- Extraction was performed as described previously (Itkin et al., 2011).
- In brief, 100 mg freeze-dried tissue was extracted with 1 mL 80% methanol/water (v/v) containing 0.1% formic acid.
- The mixture was vortexed for 30 s, sonicated for 30 min at 4C, vortexed again for 30 s, centrifuged (20 000 g, 10 min, 4C), and filtered through a 0.22-mm polytetrafluoroethylene membrane filter.
- SGA profiling of tomato tissues was performed by LC-MS using the SCIEX Triple Quad 5500 LC-MS/MS System with a UPLC column connected online to a photodiode array detector (Shimadzu).
- Separation of metabolites and detection of the eluted compound masses were performed as described previously (Zhu et al., 2018).
- All samples were analyzed in biological triplicate.
### RNA Extraction and qRT–PCR 
- Both MicroTom and transgenic fruits were harvested at Br3, and fruit pericarp was ground into a fine powder using liquid nitrogen.
- RNA extraction and cDNA synthesis were performed as described previously.
- qRT–PCR was performed using the Bio-Rad CFX384 Real-Time System, following the manufacturer’s instructions.
- With SlUBI as an internal control, the relative expression level of each gene was calculated using the DCt method.
- The primer pairs for qRT–PCR were blasted at the NCBI database to ensure primer specificity (see Supplemental Data 6).
### Vector Construction and Generation of Transgenic Lines 
- The overexpression constructs used for Agrobacterium-mediated tomato plant transformation were built using GoldenBraid cloning (Sarrion- Perdigones et al., 2013) and Gateway Cloning Technology (Curtis and Grossniklaus, 2003).
- For fruit-specific expression, full length coding sequence (CDS) was introduced into pBin18-E8-GW by Gateway Cloning (Ying et al., 2020).
- We used the GoldenBraid system to generate the 35S promoter–TF-35S terminator as one transcriptional unit; a kanamycin resistance gene under the control of the NOS promoter and the NOS terminator was also included.
- A plasmid with the correct insertion was introduced into Agrobacterium tumefaciens strain EHA105, and tomato transformation was performed as described previously (Ying et al., 2020).
### Subcellular Localization 
- Tobacco (Nicotiana benthamiana) used in this study was grown in the greenhouse with a light/dark photoperiod of 16/8 h at 25C.
- Determination of the subcellular localization of individual TFs fused to the GFP fluorescent reporter was performed in N.
- benthamiana leaf protoplasts as described previously (Deng et al., 2018).
- In brief, released protoplast cells from leaves of 3- to 4-week-old tobacco plants were isolated and transformed via the PEG-mediated protoplast transfection method (Deng et al., 2018).
- Full-length cDNA was fused with GFP in pBI101.3, and pBI101.3-SlTF and pBI101.3 were individually transiently transformed into the protoplasts of N.
- benthamiana leaves.
- After one night of growth, DAPI was used to stain the nucleic acids of the protoplasts.
- Signals from GFP and DAPI were visualized with a laser scanning confocal microscope (Zeiss Cell Observer SD).
### Transient Dual Luciferase Reporter Assay 
- Promoter sequences were amplified from genomic DNA using PCR and inserted upstream of the Luciferase (LUC) CDS using the GoldenBraid 2.0 cloning strategy to yield promoter-LUC reporter vectors.
- For an internal control, the expression of the Renilla (REN) gene was driven by the CaMV35S promoter in a reporter vector.
- The CDS of SlTF was cloned into the pUPD2 vector using the GoldenBraid 2.0 cloning strategy to generate an overexpression construct named 35S-SlTF.
- The empty vector P35S-T35S was used as the negative control (CK).
- A.
- thaliana (Columbia-0) used in this studywas grown in the greenhouse with a light/dark photoperiod of 16/8 h at 22C.
- The dual luciferase reporter assay was performed as described previously (Deng et al., 2018).
- In brief, protoplasts used for transfection were isolated from 4- to 5-week-old A.
- thaliana leaves.
- Protoplast co-transfection assays were performed using the reporterplasmids and the internal control vectors.Resultswereanalyzed and quantified by flow cytometry 16 h after protoplast transfection.
- Luciferase activity was detected using the dual luciferase reporter assay system (Promega) with a Synergy H1 hybrid multimode microplate reader (BioTek).
- Expression was expressed as the ratio of LUC to REN activity.
### Statistics 
- For comparison of individual treatments with their relevant controls, unpaired two-tailed Student’s t-tests were used, and P % 0.05 was considered significant.
- To compare measurements of multiple treatments with one another, we performed univariate ANOVA followed by the post-hoc Tukey’s test of multiple pairwise comparisons to determine group differences using GraphPad Prism version 8 (Swift, 1997).
## Accession Numbers 
- Tomato genome sequence data for this article were downloaded from the SGN (https://solgenomics.net/).
- The raw values obtained from the metabolomic datasets are available in Supplemental Data 1 (associated figures: Figures 2A, 2C, 2E, and 3, Supplemental Figure 1A, and Table 1).
- RNA-seq datasets for the transcriptome analysis are available at the Genome Sequence Archive at the Big Data Center under accession numbers CRA001723 and CRA001712 and are publicly accessible at http://bigd.
- big.ac.cn/gsa (Wang et al., 2017) (associated figures: Figures 2B, 2D, 2F, 4A, and 4B, Supplemental Figures 1B, 2–6 and 11).
- Sequence data for the phylogenetic analysis can be found in Supplemental Table 2.
- If any datasets are unavailable through the links above, they can be obtained from the corresponding author upon request.
## Fig {#Fig} 
> [Fig1](https://ars.els-cdn.com/content/image/1-s2.0-S1674205220301830-gr1_lrg.jpg)  
> [Fig2](https://ars.els-cdn.com/content/image/1-s2.0-S1674205220301830-gr2_lrg.jpg)  
> [Fig3](https://ars.els-cdn.com/content/image/1-s2.0-S1674205220301830-gr3_lrg.jpg)   
> [Fig4](https://ars.els-cdn.com/content/image/1-s2.0-S1674205220301830-gr4_lrg.jpg)   
> [Fig5](https://ars.els-cdn.com/content/image/1-s2.0-S1674205220301830-gr5_lrg.jpg)  
> [Fig6](https://ars.els-cdn.com/content/image/1-s2.0-S1674205220301830-gr6_lrg.jpg)    