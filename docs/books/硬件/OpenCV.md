# OpenCV4快速入门

## OpenCV4配置

Clion需要先使用Cmake对OpenCV进行一次编译。所以简单一点还是使用Vs了。另外C++和Python都配置一下。

- Python的很简单，直接在[Archived](https://www.lfd.uci.edu/~gohlke/pythonlibs/)镜像网站上下载对应版本的OpenCV，然后再环境（我是Anaconda的虚拟环境）中使用 `pip install whl文件名`就可以轻松安装了。
  - Opencv直接使用pip安装很容易出错
- C++的配置需要分别配置电脑的环境变量以及VS中的属性参数，能够让外部依赖选择到opencv的文件。另外可能还需要再System32下包含进dll文件。

