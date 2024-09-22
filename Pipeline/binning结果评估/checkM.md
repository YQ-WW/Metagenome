---
tags:
  - Project/主线/宏基因组
---
[[🧬Metagenome]]
# 1. checkM
![[checkM.png|400]]
CheckM1即CheckM，通过使用在系统发育谱系中普遍存在的单拷贝基因集 (single-copy)来估计基因组的完整度和污染度。由于CheckM使用的标记基因是细菌和古菌特有的，因此适用于评估**细菌和古菌**基因组质量，不适合真核生物和噬菌体。
- CheckM官网http://ecogenomics.github.io/CheckM/
- Github主页https://github.com/Ecogenomics/CheckM/wiki
## 1.1 checkM的原理
基于数据库中构建好的单拷贝基因集和进化树，将bin定位到进化树中找到参考物种，基于谱系特异的marker gene(单拷贝)，进行完整性和污染度进行评估。![图片|700](https://mmbiz.qpic.cn/sz_mmbiz_jpg/2VUzp7XpZWuqZmOzeVgMEiabLz1fr94v26UdqeapUqJoTuu32efJM1Km54iafZAicMM3AB9eT8GQ2nJ55cPswCIIg/640?wx_fmt=other&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)![[checkm原理翻译.png|700]]
这张图片是一个流程图，描述了基因组参考数据集的质量控制和分析过程。核心内容包括：
1. **参考基因组注释**：从所有参考基因组注释中筛选出可信赖的基因组。
2. **质量控制**：对选择的基因组进行质量检查。
3. **推断谱系特异性标记基因**：识别出能够表示不同遗传谱系（族群）的特定标记基因。
4. **计算统计数据**：通过汇总信息来估算比如GC含量、N50等统计指标，以评价序列质量。
5. **推断位置关联信息**：根据给定的参数确定各个放置在进化树上的位置。
6. **使用谱系特异性估算器估算品质**：利用与遗传谱系相关联的资料来评估假设出来（putative）品质。 例子方面，如果我们有多个微生物群落样本中提取到的DNA序列，并且想要构建每个微生物在进化树上位置的模型，则可以按照该流程图所示步骤执行。首先需要确保你有高品质、经过验证并且已经被广泛接受为准确无误得一套“参考基因组”。然后通过各种统计方法和工具去处理这些数据，并最终获得既能代表其遗传背景也符合线粒体DNA证据支持度很高得分类学地位推断。 整个流程结果可能会生成一个带有详尽信息（例如: 贯穿整条链路都强调了"quality estimate"即品质预测）及实际应用情况（如何处理实测数据文件） 的报告或数据库。


## 1.2 选择checkM
分箱结果可以使用 checkM 检查完整性和污染度
## 1.3 code
### Bioinfor 生信云
```shell
# 运行checkM  
checkm lineage_wf \
--threads 16 \ # 线程  
--tmpdir ./ \ # tmp目录路径  
--extension fa \ # 序列文件后缀  
bins \ # 输入，分箱结果目录  
checkm \ # 输出目录  
> checkM.sh.log 2>&1 # 存储日志
```
### CSDN
```shell
checkm lineage_wf -t 16 -x fa --nt --tab_table -f bins_qa.txt metabat_bins bins_qa_result 
 
#-t 线程数
#-x 输入的文件格式后缀为fa，即分箱的结果，如bin.1.fa
#--nt 检测序列为核酸序列
#--tab-table 输出文件格式，为txt或tsv
#-f 输出文件
#metabat_bins 存放metabat2分箱结果的文件；
#bin_qa-result 输出文件
```


# code---北大课程
![[乔雪皎CheckM的命令及使用.png]]
# code---公众号
```shell
# 运行checkM  
checkm lineage_wf \
--threads 5 \  # 线程  
--tmpdir ./ \  # tmp目录路径  
--extension fa \  # 序列文件后缀  
bins \  # 输入，分箱结果目录  
checkm \  # 输出目录  
> checkM.sh.log 2>&1  # 存储日志
```



# 参考
> GitHub链接
> http://ecogenomics.github.io/CheckM/