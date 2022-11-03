# OpenCV4快速入门

## OpenCV4配置和基础

### Clion+MinGW配置

1. 安装MinGW
   - Windows中的配置基于MinGW进行，注意不能选择Win32版本而是要选择posix版本，不然会在make的时候出现线程冲突无法解决。

2. 安装Cmake
   - 版本有讲究的，打开Clion可以看一下需要的版本，太新的版本和MinGW编译器无法对应。比如我使用的就是Cmake3.20+MinGW8.1-posix-seh。
3. Clion安装并且配置环境，跑一下HelloWorld例程，编译成功就可以了。
4. 下载OpenCV和对应的contrib压缩包，打开Cmake，选择MinGW方法和默认的编译器进行编译。
   1. 路径选择sources，目标新建一个mingw-build文件夹就可以了。
   2. 这一步出错方式很多，但是所幸使用MinGW可以避开很多错误。
5. 勾选world,NON...,在EXTRA_PATH下添加contrib的路径，然后点击configure，直到没有报错和红色，点击Generate。
6. 在生成的编译文件夹中进行mingw32-make编译，这一步如果选对了版本应该不会出错的。不然的话各种神奇的错误。
7. 下一步是install。
8. 系统中添加生成的install文件下的\x64\mingw\bin。Clion的路径中添加mingw-build。

### VS22配置

1. 基本的思路和上一个相似，虽然不推荐使用VS22，感觉上VS17更加方便一些。虽然但是，本篇的环境和版本使用的是VS22+Cmake3.23版本。

2. 基础的opencv配置甚至不需要编译，直接官网上下载了OpenCV的安装版本之后，就生成了基础的build文件，其中包含了大部分的常用openCV库可以直接使用了。想要使用contrib的部分则需要Camke进行编译。基本步骤和上一个类似，只是Cmake中需要选择VS17 2022这个选项，如果显示未找到那就说明安装出错了或者VS版本选择错误了。找到之后的步骤和Clion中的Cmake编译就完全一样了。

   1. 只有一些文件下载错误，只需要网上找到文件然后放到moudule下就可以了。

3. 生成了新的build文件之后，在VS中打开其中的OpenCV.sln，进行一次生成（其实就是make+install）。结束之后对于生成的install文件夹进行绑定。

   - 需要绑定的是属性中的包含目录、库目录以及连接器。

   - C++的配置需要分别配置电脑的环境变量以及VS中的属性参数，能够让外部依赖选择到opencv的文件。另外可能还需要再System32下包含进dll文件。

4. ImageWatch插件:OpenCV专门为VS开发的插件，可以预览图片。

### Ubuntu配置

### RaspberryPi配置

利用Python的很简单，直接在[Archived](https://www.lfd.uci.edu/~gohlke/pythonlibs/)镜像网站上下载对应版本的OpenCV，然后再环境（我是Anaconda的虚拟环境）中使用 `pip install whl文件名`就可以轻松安装了。

- Opencv直接使用pip安装很容易出错

### OpenCV的模块架构

基本include下一个文件夹对应一个重要的OpenCV模块，samples文件夹中存放了相关的例程。

测试一下例程中的edge边缘检测。



## 数据载入、显示与保存

1. C++的OpenCV数据结构本质上就是创建了一个名为Mat的类型，
