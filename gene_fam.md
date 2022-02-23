# 基因家族鉴定分析操作手册
## 1.数据准备
基因家族鉴定与分析所需数据一般包括基因组序列fasta，基因组注释文件gff，编码序列cds和蛋白序列pep。  
Ensembl下载地址：http://plants.ensembl.org/index.html  下载方法可参考：https://www.omicsclass.com/article/58  
phytozome（JGI）下载地址：https://phytozome.jgi.doe.gov/pz/portal.html  下载方法可以参考：https://www.omicsclass.com/article/50  
NCBI官网下载：https://www.ncbi.nlm.nih.gov/  下载方法可参考：https://www.omicsclass.com/article/497  
常用下载工具包括：wget, curl, datasets等，如果要从NCBI批量下载基因组数据，推荐使用专门的下载工具datasets，如要下载所有柑橘基因组
```
datasets download genome taxon "citrus" --dehydrated
#下载会得到一个压缩文件ncbi_dataset.zip，包含了需要下载的文件
unzip ncbi_dataset.zip
datasets dehydrate --directory .
```
## 2.基因家族鉴定  
1. 结构域hmmer鉴定
查找自己研究的基因家族含有什么结构域信息，文献中来或者上pfam数据库中直接搜索。如果研究的是转录因子，用plantTFDB鉴定http://planttfdb.gao-lab.org/。
pfam：http://pfam.xfam.org/  
2. blast鉴定
如果研究的基因家族未找到结构域信息，可通过blast直接搜索相似序列，再根据比对情况、功能注释等信息确定候选对象。

## 3.进化树分析  
1. 基于结构域构建进化树
2. 基于基因全长构建进化树
3. 进化树显示与美化
   a. Evolview v2: https://www.evolgenius.info/evolview-v2/
   b. iTOL: https://itol.embl.de/

## 4.MEME 搜索基因motif分析
MEME(Motif-based sequence analysis tools)大家都很了解，是搜索DNA或者蛋白质的motif常用工具，结果输出一般是有四个文件，motif的图形展示文件（LOGO），txt文本，html的网页信息文件及xml格式文件。  
MEME可在线分析，也可本地在服务器上进行。

## 5.基因结构分析- 外显子内含子等作图
GSDS网址：http://gsds.gao-lab.org/   
![](https://www.omicsclass.com/image/show/attachments-2018-10-JQEPqA8I5bd6dbd9b9360.jpg)

