# Openlaw Tools
一个使用各类文本分析方法，来分析openlaw裁判文书的工具。

### 使用环境
* Anaconda 2019.10版本（至少是python3的发行版。）
* python3(所有ipynb文件在python3.7环境下写成。)
* 所需要的包都在requirements.txt里，若要单机使用：
> pip install -r requirements

### 使用方法
* 打开jupyter notebook，一路执行下去就好，会有交互的提示。

### 所要准备好的文件
* 从Openlaw（或者Openlaw API）中所下载下来的excel文件。
* 举例文件见于该repo中。

### 分文件解说
1.裁判文件API
* 此步借助openlaw API的平台来得到文书：http://develop.openlaw.cn/index.jsp
* 个人账号文书的每日上限是1000份文书，因此请控制下列代码运行时的条件。
