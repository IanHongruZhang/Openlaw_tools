# Openlaw Text-Analysis Tools
一个使用各类文本分析方法，来分析openlaw裁判文书的工具。
> https://github.com/IanHongruZhang/Openlaw_tools

目前（2019-11-18）主要实现的功能有
* 筛去不符文本。
* 法条信息查找。
* 案件信息结构化重构。
* 使用正则表达式，对重要信息发掘并转换成html格式阅读。
* 词频分词。
* 自动摘要提取。（基于HanLp)
* 词语共现。（基于HanLp)
* 人名查找。（基于HanLp)
* 地名查找。（基于HanLp)
* LDA文书信息聚类
* Kmeans文书信息聚类
* Repeated-Bisection聚类（基于HanLp)

### 使用环境
* Anaconda 2019.10版本（至少是python3的发行版。）
* python3(所有ipynb文件在python3.7环境下写成。)
* 所需要的包都在requirements.txt里，若要单机使用：
> pip install -r requirements

### 使用方法
* 打开jupyter notebook，一路执行下去就好，会有交互的提示。

### 所要准备好的文件
* 从Openlaw（或者Openlaw API）中所下载下来的excel文件。
* 举例文件见于该repo中，如正当防卫、职业打假人等原表。

### 分文件解说
1.裁判文件API
* 此步借助openlaw API的平台来得到文书：http://develop.openlaw.cn/index.jsp
* 个人账号文书的每日上限是1000份文书，因此请控制下列代码运行时的条件。


### 后续工作
* 做出web网页端的工具集成
