## 物种分类学注释
分类学(taxonomy): 是一门研究生物类群间的异同以及异同程度，阐明生物间的亲缘关系、进化过程和发展规律的科学。  
- 主要分为细菌、古菌和真核生物三大类 
- 常用七级分类法：界(Kingdom)、门(Phylum)、纲(Class)、目(Order)、科(Family)、属 (Genus)、种(Species)
![[Pasted image 20240919164726.png]][A new view of the tree of life | Nature Microbiology](https://www.nature.com/articles/nmicrobiol201648)

## 物种注释数据库
- NCBI——NR非冗余序列，NCBI发布的序列包含物种Taxonomy ID  
- MetaPhlAn2——整理已发表基因组Marker基因数据库  
- GTDB——基因组细菌120/古菌122单拷贝基因  
- GreenGenes/RDP——原核生物核糖体(16S)数据库  
- SILVA——原核、真核核糖体(16/18S)数据库  

## 物种注释方法
### 方法
- 比对方法：与有物种注释的序列数据库比对，通过相似度进行物种注释；这种方法受限于数据库，且比对结果不准确。常用blast、diamond等。  
- LCA(Lower Common Ancestor最低共同祖先) ：此类方法常基于K-mer进行分类注释；目前认为方法较准确，但是注释到的物种信息很少，常用软件有Kraken系列、RDP classifier、Sintax等。

### Kraken
- [Kraken：使用精确比对的超快速宏基因组序列分类软件 (qq.com)](https://mp.weixin.qq.com/s/-02ebEOU3yk82xbYVFlbVQ)
- LCA(lower common ancestor):
  为了对序列进行分类，序列中的每个k-mer被映射到数据库中包含该k-mer基因组的最低共同祖先（lowest common ancestor, LCA）。与序列的k-mers相关的分类群以及分类群的祖先形成了一般分类树的修剪子树，用于分类。在分类树中，每个节点的权重等于与节点的分类单元相关联的序列中的k-mer的数量。通过在路径中添加所有权重来对分类树中的每个根到叶（root-to-leaf, RTL）路径进行评分，并且分类树中的最大RTL路径是分类路径（以黄色突出显示的节点）。该分类路径的叶子（分类树中的橙色，最左边的叶子）是用于查询序列的分类。
  ![[Pasted image 20240919165816.png]]
- 基于三个模拟宏基因组的分类程序准确性和速度比较
  ![[Pasted image 20240919170250.png]]

### Kraken2
