![M6Okh8.png](https://s2.ax1x.com/2019/11/18/M6Okh8.png)

# Openlaw Text-Analysis Tools
### 开发初衷
打造一个使用各类文本分析方法，来分析openlaw法律裁判文书的工具。
> https://github.com/IanHongruZhang/Openlaw_tools

由于开发者本人为一名数据新闻编辑，此工具是为制作数据新闻的稿件而制作。详情请查阅澎湃新闻·美数课栏目的所有稿件，以及美数课栏目的网站。

> http://projects.thepaper.cn/thepaper-cases/839studio/?cat=4

### 可能曾经使用过该工具产生的稿件
* 《为何有了“新解释”，纠错夫妻债务纠纷的历史遗案还那么难？》

> https://www.thepaper.cn/newsDetail_forward_3214161

* 《这是坑｜判决书中的微商骗局套路，微商可能比你更容易上当》

> https://www.thepaper.cn/newsDetail_forward_3139674

* 《图解｜中国式遗嘱：忌立遗嘱心态改观，遗嘱纠纷几时休》

> https://www.thepaper.cn/newsDetail_forward_2060254

* 《巨额来电套路深？图解462份判决书中的电信诈骗》

> https://www.thepaper.cn/newsDetail_forward_1902196  

目前（2019-11-18）主要实现的功能有
* 筛去不符文本
* 法条信息查找
* 案件信息结构化重构
* 使用正则表达式，对重要信息发掘并转换成html格式阅读
* 词频分词
* 自动摘要提取（基于HanLp)
* 词语共现（基于HanLp)
* 人名查找（基于HanLp)
* 地名查找（基于HanLp)
* LDA文书信息聚类
* Kmeans文书信息聚类
* Repeated-Bisection聚类（基于HanLp)

### 使用环境
* Anaconda 2019.10版本（至少是Python3的发行版)。
* Python3(所有ipynb文件是在Python3.7环境下写成)。
* 所需要的包都在requirements.txt里，若要单机使用：
> pip install -r requirements

* 非常非常感谢大佬hankcs对HanLp的python化工作，让本工具的最后几个部分能够得以实现。
* 基于Apache License Version 2.0的守则，在此显式注明我对HanLp的引用，以及我对大佬的崇敬仰慕之情。
> https://github.com/hankcs/HanLP

### 使用方法
* 打开jupyter notebook，一路执行下去就可以，会有交互的提示。

### 所要准备好的文件
* 从Openlaw（或者Openlaw API）中所下载下来的excel文件。
* 举例文件见于该repo中，如正当防卫、职业打假人等原表。

### 分文件解说

> 所有的工具里，都会有“本地操作”和“远程操作”两种模式。两种本质上是一样的，“远程操作”为远程使用jupyter notebook服务器端所考虑，本地操作中会弹出一个文件选择窗口(tkinter)，然后可以从电脑中任一路径选择文件导入。而远程操作为默认文件与工具在同一目录下，直接选择文件编号导入。

> 所有最后都会生成相应.xlsx表格，并支持导出表格。

1.裁判文书API（对应第一步）
* 此步借助openlaw API的平台来得到文书：http://develop.openlaw.cn/index.jsp。
* API的token，请按照API平台上的来申请。
* 个人账号文书的每日上限是1000份文书，因此请控制下列代码运行时的条件。
* 获取文书的方法，也可以经由Openlaw的网站上按照条件下载，每个账号每天的限制为1000份。

2.筛去不符文书（对应第三步）
* 此工具里包括三个处理工具，运行所有模块后，直接运行下面三个处理工具即可。
* 长度筛选器是指，在openlaw文书表格中，任意一列若为*空白（None字符)或者字数太少*。则直接筛去。
* 正则表达式筛选器是指，在openlaw文书表格中，筛去不含关键字的案件。（如以“正当防卫“关键字搜索来的案件表格，有些案件通篇没有正当防卫这4字，则筛去）
* 余弦相似筛选器是指，筛去与目标案件在词袋模型余弦相似度（欧氏距离）上太远的案件。
>上述方法可连续使用，最终旨在得到一个清理干净的文书表格。

![M6X7i6.jpg](https://s2.ax1x.com/2019/11/18/M6X7i6.jpg)

3.法条信息抽取（对应第四步）
* 抽取所有案件判决中，判决最终所依据的法条细则，包括各法条细则（如《中华人民共和国刑法》第231条）。
* 抽取所有的法条（如《中华人民共和国刑法》、《中华人民共和国物权法》等）。


![M6XoIx.jpg](https://s2.ax1x.com/2019/11/18/M6XoIx.jpg)

4.罪名提取（只适用于刑事案件，对应第五步）
* 抽取罪名，以及罪名的数量。

![M6XbRO.jpg](https://s2.ax1x.com/2019/11/18/M6XbRO.jpg)

5.提取重要表达（对应第六步）
* 使用正则提取方法，高亮出所有重要的表述。
* 支持将所有的重要表述，导出成.html文件，如下图所示。

![M6XOQe.jpg](https://s2.ax1x.com/2019/11/18/M6XOQe.jpg)

6.切取句子得到词频（对应第七步）
* 使用HanLp的HanLP.segment()方法，得到一列中所有的词频。

![M6XHJK.jpg](https://s2.ax1x.com/2019/11/18/M6XHJK.jpg)

7.使用HanLp得到摘要（对应第八步)
* 使用HanLp的HanLP.extractSummary()方法，得到一段话中指定数量的摘要。

![M6XqzD.jpg](https://s2.ax1x.com/2019/11/18/M6XqzD.jpg)

8.词语共现（对应第九步）
* 使用前面得到的切词表、以及原案件表中的文字，得到高频词在一个案件中共同出现的次数。
* 用以进一步架构语义网络。

9.人名&地名&组织名查找（对应第十、十一步）
* 切分出人名、地名、组织名。
* 使用HanLP.newSegment().enableNameRecognize()以及enablePlaceRecognize()、enableOrganizationRecognize()。

![M6X5ZR.jpg](https://s2.ax1x.com/2019/11/18/M6X5ZR.jpg)

10.文本聚类（对应十二、十三、十四步）
* 十二步为LDA聚类算法
* 十三步为Kmeans算法
* 十四步为HanLp自带的Repeated-Bisection（重复二分法）
> 关于该算法介绍：https://github.com/hankcs/HanLP/wiki/%E6%96%87%E6%9C%AC%E8%81%9A%E7%B1%BB

### 后续工作
* 做出web网页端的工具集成。
* 使用深度学习框架，进行监督学习的测试。
