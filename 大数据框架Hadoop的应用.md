# 大数据框架Hadoop的应用
***

## 一.搭建Hadoop分布式计算框架
***

## 二.通过Map-Reduce实现中文网页数据的K-means聚类
### 步骤1：下载网页数据并生成原始数据文件集合
1. 可通过下载数据具有
2. 可爬虫获取

### 步骤2：对原始数据提取中文部分，进行分词、去停用词等预处理
#### 大体内容
1. 中文词分词
2. 停用词：中文词去“的”等，可用听用词表

#### 确定输入
1. 数据：原始网页数据
2. 格式：网页编号 网页内容

#### 子步骤2.1.：分词，去停用词，统计词频
##### Map模块 （映射）
1. 输入格式： 网页编号 -> 网页内容
2. 输出格式： 单词 | 网页编号 -> 1 （1指出现了一次）

##### Reduce模块 （sort + 聚集）
1. 输入格式： 单词 | 网页编号 -> 1
2. 输出格式： 单词 | 网页编号 -> 单词在网页编号中出现的次数

#### 子步骤2.2.：统计每个网页中单词的占比
##### Map模块
1. 输入格式：单词 | 网页编号 -> 单词在网页编号中出现的次数
2. 输出格式：网页编号 -> 单词 | 1

##### Reduce模块
1. 输入格式：网页编号 -> 单词 | 1
2. 输出格式：单词 | 网页编号 -> 单词在网页编号中出现的次数/网页的总单词数

#### 子步骤2.3. ：统计单词出现的网页个数、TF-IDF值、建立词表

##### TF-IDF
1. TF值
在单个网页出现的次数
2. IDF值
单词在多少个网页出现过

##### Map模块
1. 输入格式：单词 | 网页编号 -> 单词在网页编号中出现的次数/网页的总单词数
2. 输出格式：单词-> 网页编号 | 单词在网页编号中出现的次数/网页的总单词数

##### Reduce模块
1. 输入格式：单词-> 网页编号 | 单词在网页编号中出现的次数/网页的总单词数
2. 输出格式：单词 | 网页编号 -> TF-IDF值
 
### 步骤3：如何构造网页特征向量？

#### 子步骤3.1.：构造网页向量
##### Map模块
1. 输入格式：单词 | 网页编号 -> TF-IDF值
2. 输出格式：网页编号 -> 单词 | TF-IDF值

##### Reduce模块
1. 输入格式：网页编号 -> 单词 | TF-IDF值
2. 输出格式：网页编号 -> 单词编号1 | TF-IDF值1 & 单词编号2 | TFIDF值2 &......
3. （将单词换成单词编号是为了便于训练）


### 步骤4：如何在Hadoop平台实现K-means算法迭代？

#### 子步骤4.1.： 实现K-means算法、迭代求解知道满足要求
##### Map模块
1. 输入格式：网页编号 -> 单词编号1 | TF-IDF值1 & 单词编号2 | TFIDF值2 &......
2. 输出格式：网页对应中心点编号 -> 单词编号1 | TF-IDF值1 & 单词编号2 | TFIDF值2 &......
##### Reduce模块
1. 输入格式：网页对应中心点编号 -> 单词编号1 | TF-IDF值1 & 单词编号2 | TFIDF值2 &......
2. 输出格式：网页对应中心点编号 -> 新的中心点向量

### 步骤5：判断每个网页属于哪个聚类中心？

#### 子步骤5.1.：输出每个网页对应中心点编号
##### Map模块
？？？？
##### Reduce模块
？？？？

### 步骤6：输出数据计算得到每个簇的网页结果

### *关注点
#### 如何构造网页特征向量
##### 深
1. 先进算法表达网页特征（磁带模型）
2. 考虑向量和数据集数量
##### 浅
1. 能用
#### 如何在Hadoop平台实现K-means算法迭代？
1. 多个map，多个reduce，怎么使用

***
## 三.最首要的确认输入输出
### 1. 输入输出不清楚时不要开始工作
### 2.输入
1） 原料是什么

### 3.输出
1） 目的是什么
