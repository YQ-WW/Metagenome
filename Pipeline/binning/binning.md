---
tags:
  - Project/主线/宏基因组
---
[[🧬Metagenome]]
# 1. def-binning
宏基因组分箱（Binning）是将宏基因组测序得到的混合了不同微生物的序列reads或序列组装得到的contigs或scaffolds按物种分开归类的过程。这些分开归类的序列被称为宏基因组组装基因组（metagenome-assembled genomes，MAGs)。传统的单物种全基因组序列都是经纯培养之后，再进行全基因组de novo测序才获得的，但是环境中存在着大量的不可培养微生物（uncultured candidate bacterial species，未培养候选菌种），而宏基因组分箱及相关技术不仅有助于获得不可培养微生物的基因组序列，还有以下诸多功能：（1）发现新物种，预测新物种基因，利用现有数据库分析新物种的功能；（2）扩充微生物基因组数据库，增加微生物多样性，提高宏基因组数据reads mapping率（检出率）；（3）有助于宏基因组技术开发；（4）助力“感兴趣”微生物群结构和功能的研究；（5）为菌群的分类和功能描述提供了更多的解决方案。早在2011年，science上的一篇文章就用了宏基因组Binning技术对来自牛瘤胃的样本进行了宏基因组测序研究。该研究从268 Gbp的宏基因数据中成功Binning出了15个不能培养的微生物的全基因组序列[1]。

从那以后，宏基因组Binning技术开始被更多的人关注和重视，也逐渐出现了很多宏基因组Binning相关的工具。Metabat是近几年所有分箱工具中最受欢迎的工具（引用达460+）。2019年发表在PeerJ上的新版Metabat2更是在完成度、效率等多方面均优于Metabat和同类工具 [2-3]。仅在2019年当年Metabat2就已经被Cell、Nature Biotechnology、Genome Biology等多篇高水平期刊引用 [4-6]。因此微科盟从众多分箱工具中选择Metabat2进行分箱。不仅如此，微科盟宏基因组分箱分析流程种使用的每一个软件都是根据效率、准确度等多个参数从众多同类软件中精挑出来的，例如序列组装工具Megahit，Bin质检工具Checkm，功能取预测工具Prokka，蛋白比对工具Diamond等等。

# 2. binning的pipeline
## 2.1 实验流程
![[binning实验流程.png]]

## 2.2 数据分析流程
[宏基因组分箱_微科盟_结题报告 (bioincloud.tech)](https://www.bioincloud.tech/cloudir/reports/binning/index.html#a2)
### 2.2.1 数据质控
测序得到的原始数据会存在一定比例的低质量数据，为了保证后续信息分析结果的准确可靠，首先要对原始数据进行质控及宿主过滤，得到有效数据[7]。分析中将使用Kneaddata软件彻底清除原始数据中的Illumina接头序列、低质量的序列片段和较短序列。质控前和质控后，会用FastQC来检测质控的合理性和效果。
==师兄建议Fastp来解决==

### 2.2.2 去除宿主
质控处理后的数据通过Bowtie2软件[9]比对到宿主的基因组(整合到了Kneaddata软件里)，没有比对到的序列被保留下来做后续分析。

### 2.2.3 binning
- 对于每个样本，运用Megahit软件，将样本去宿主基因后的clean reads进行组装（megahit默认组装参数），得到contigs；
- 运用Bowtie2进行建索引和序列比对获得clean reads在contigs中的比对信息；
用Samtools软件[10]对比对结果进行格式转换和排序；
- 用Metabat2自带的jgi_summarize_bam_contig_depths程序计算contigs深度；
挑选长度大于1500bp的contigs，结合上一步得到的contigs深度，用Metabat2对contigs进行分箱；
- 用RefineM [11] 对得到的bins进行提纯，去除bins中污染度较高的contigs

### 2.2.4 1. 去冗余和筛选
[[CheckM]
合并所有样本中得到的bins，用CheckM[12]中的lineage_wf流程评估bins的完成度和污染度，并用dRep[13]软件对bins进行去冗余，挑选完成度大于75%，同时污染度小于25%的bins用于后续分析(dRep 默认参数)。

# 3. 软件实操
## MetaBAT
[宏基因组binning：MetaBAT-腾讯云开发者社区-腾讯云 (tencent.com)](https://cloud.tencent.com/developer/article/1991327)


# 参考链接
[宏基因组分箱_微科盟_结题报告 (bioincloud.tech)](https://www.bioincloud.tech/cloudir/reports/binning/index.html)

https://www.bioincloud.tech/cloudir/reports/bac_genome/bacdrafgenome/FiguresTablesForReport/readme/nr.readme.html

