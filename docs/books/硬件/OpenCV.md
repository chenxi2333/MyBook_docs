# OpenCV4快速入门

## OpenCV4配置

Clion需要先使用Cmake对OpenCV进行一次编译。所以简单一点还是使用Vs了。另外C++和Python都配置一下。后来发现VS虽然能用但是想要使用Contrib还是绕不开编译，而VS的编译一直报错，只能最后又

- Python的很简单，直接在[Archived](https://www.lfd.uci.edu/~gohlke/pythonlibs/)镜像网站上下载对应版本的OpenCV，然后再环境（我是Anaconda的虚拟环境）中使用 `pip install whl文件名`就可以轻松安装了。
  - Opencv直接使用pip安装很容易出错
- C++的配置需要分别配置电脑的环境变量以及VS中的属性参数，能够让外部依赖选择到opencv的文件。另外可能还需要再System32下包含进dll文件。
- ImageWatch插件:OpenCV专门为VS开发的插件，可以预览图片。
- 树莓派上安装Python版本的OpenCV即可。
  - 安装libopencv-dev和pyton3-opencv库就可以了。不需要解压或者使用Cmake编译。

- 在Ubuntu环境下使用Cmake安装：大概就是需要把各种库下载下来然后解压并且Cmake一下。
- opencv_contrib拓展模块中包含了很多使用的模块，需要安装。这个库
