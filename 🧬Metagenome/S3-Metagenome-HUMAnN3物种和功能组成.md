#Project/主线/宏基因组 
[[🧬Metagenome]]
## MetaPhlAn4
MetaPhlAn4 (metagenomic phylogenetic analysis,宏基因组系统发育分析，2012-2023)3MetaPhlAn4基于多标记基因的宏基因组物种组成定量文章解读软件使用
[biobakery/MetaPhlAn: MetaPhlAn is a computational tool for profiling the composition of microbial communities from metagenomic shotgun sequencing data (github.com)](https://github.com/biobakery/MetaPhlAn)
![Pasted image 20240919110333.png](./attachments/Pasted%20image%2020240919110333.png)
![Pasted image 20240919110442.png](./attachments/Pasted%20image%2020240919110442.png)
![Pasted image 20240919110501.png](./attachments/Pasted%20image%2020240919110501.png)

- 软件安装代码见1soft_db.sh或2pipeline.sh  
- 除非只关注物种组成，否则MetaPhlAn很少单独使用
- HUMAnN3整合了MetaPhlAn4软件，可实现一条命令完成物种、功能、以及功能对应物种组成三个文件，多角度挖掘宏基因组数据

## HUMAnN3: The HMP Unified Metabolic Analysis Network 3
HUMAnN是基于宏基因组、宏转录组数据分析微生物通路丰度的有效工具。这一过程称为功能谱，目的和意义：
- 描述群体成言代谢潜能
- 回答微生物群体成员可能干什么，或在干什么的问题