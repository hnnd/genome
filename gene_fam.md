# 基因家族鉴定分析操作指南  
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
![tree](https://www.omicsclass.com/image/show/attachments-2019-02-RbUXm4HJ5c661bede4e37.jpg)

## 4.MEME 搜索基因motif分析  
MEME(Motif-based sequence analysis tools)大家都很了解，是搜索DNA或者蛋白质的motif常用工具，结果输出一般是有四个文件，motif的图形展示文件（LOGO），txt文本，html的网页信息文件及xml格式文件。  
MEME可在线分析，也可本地在服务器上进行。  
![motif](https://www.omicsclass.com/image/show/attachments-2018-10-eE4S9VaA5bd6dbc5cca12.jpg)

## 5.基因结构分析- 外显子内含子等作图  
GSDS网址：http://gsds.gao-lab.org/   
![GSDS](https://www.omicsclass.com/image/show/attachments-2018-10-JQEPqA8I5bd6dbd9b9360.jpg)  

## 6.基因定位到染色体  
http://mg2c.iask.in/mg2c_v2.0/  
MG2C, MapGene2Chromosom: http://mg2c.iask.in/mg2c_v2.0/  
![MG2C](https://www.omicsclass.com/image/show/attachments-2018-10-kWpPgbY35bd6dbf186274.jpg)

## 7.基因顺势作用原件分析  
Plant CARE 地址：http://bioinformatics.psb.ugent.be/webtools/plantcare/html/  
提取顺势作用原件，利用GSDS绘图：  
![cis](https://www.omicsclass.com/image/show/attachments-2018-10-D5flRWuq5bd6dc2c3d292.jpg)

## 8.基因亚细胞定位  
DeepLoc: https://services.healthtech.dtu.dk/service.php?DeepLoc-1.0  
TargetP: https://services.healthtech.dtu.dk/service.php?TargetP-2.0  

## 9.蛋白三维结构分析    
![3d](https://www.omicsclass.com/image/show/attachments-2021-04-hFGGUaNk6073f4798341d.png)   
1.同源模建 homology modeling   
相似的氨基酸序列对应着相似的蛋白质结构 ,找到与目标序列一致度≥30%已知结构作为模板代表工具: SWISS-MODEL https://swissmodel.expasy.org/   
2. Alphafold  
https://colab.research.google.com/github/deepmind/alphafold/blob/main/notebooks/AlphaFold.ipynb  可能需要翻x  
3. 第三方软件对模型评分  
模型预测出来后需要有评估软件认为合格才能用，下载PDB文件，提交到测评软件。  
SAVES：（一次性提供6个软件评估结果）https://saves.mbi.ucla.edu/ ，其中有三个显示通过即表示模型可用。多个软件判断模型好坏依据。  
1).verify 3D  
超过80%的残基拥有大于0.2的3D/1D值，则模型质量合格，低于0.2的部分需要进一步修正。  
2).procheck  
PROCHECK程序不考虑能量，只检测结构中的残基之间角度是否合理，生成Ramachandran plot。PROCHECK显示氨基酸残基核心区：91.3%，允许区：8.3%，大致允许区：0.4%，禁阻区：0%，位于可接受区的达到了100%，一般位于可接受区的氨基酸残基大于90%可以认为蛋白结构合理。  
![saves](https://www.omicsclass.com/image/show/attachments-2021-04-NZvEPcf7607fa2ca24e15.png)
3).whatcheck  
提交的蛋白结构与正常结构之间的差异，指标多，绿色多就当通过了。
4).errat  
计算0.35nm范围之内，不同的原子类型对之间形成的非键相互作用的数目（侧链）。得分>85较好，晶体可达到95，一般来说结果在91以内。
5).prove  
与预先计算好的一系列标准体积的差别，用z-score来表示，显示模版蛋白质与待测蛋白之间的匹配程度，越高越好。

## 10.基因家族共线性分析
1. mcscanX共线性分析，使用参考https://www.jianshu.com/p/740cb9eccf2b  
![mcscan](https://www.omicsclass.com/image/show/attachments-2018-10-Vq9EkoMx5bd6dbff644da.jpg)
2. 共线性结果显示 https://synvisio.github.io/  


