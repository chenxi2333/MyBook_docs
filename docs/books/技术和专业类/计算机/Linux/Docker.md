# Docker技术

> 一些参考资源：
>
> 1. [快速入门](https://docker.easydoc.net)
> 2. [Docker手册](https://docs.docker.com/get-started/)

## 导论

- 一言以蔽之：轻量化的软件打包、部署、分发的工具。

  - 容器的优势：Build once, Run Anywhere
  - 容器技术是一种虚拟化的技术，可以裁剪计算机的资源，充分利用资源去满足需要的应用。
  - Docker是容器技术的代表，容器技术是Linux下的一种手段。它对操作系统进程进行了封装隔离，节约了服务器的资源。
  - 通过Docker容器技术，可以简化开发流程：本地程序，开发好DockerFile脚本，将代码和环境依赖打包成为镜像文件，其它机器（测试、生产服务器）可以直接运行（docker run）这个镜像，不再需要各种配置。

- Docker使用的是Clinet/Sever架构，客户端向服务器发送请求，服务器负责构建、运行和分发容器。

  Docker基础组件：CLI客户端命令行、API、服务器端。
  - 客户端Client：用来构建和运行容器

  - 服务器：其中有daemon组件，用来创建、运行、监控容器，构建、存储镜像。（客户端和服务器有时候在一个机器上）

  - Docker镜像：一个模板，

    其中包含了应用程序所需要的环境，打包为image文件——可以下载，可以自己按照规范写；镜像是一个对象基类，一个模板，用户通过这个对象构建

  - Container:容器，应用程序跑在容器中

  - 镜像仓库（dockerhub就是官方的镜像仓库）:存放镜像文件的仓库。

  - 容器：镜像的实例

  - Register：存放镜像的仓库。

- 平台组成：客户端、Docker主机、镜像仓库
  - 客户端上：构建/拉取镜像、docker启动。
  - 服务端：基于镜像运行容器
  - 网络端：提供下载镜像。

## Docker安装

1. 参考官方手册[Install Docker Desktop on Linux](https://docs.docker.com/desktop/install/linux-install/#system-requirements)
2. docker的安装有engine和desktop，前者包含了虚拟机、图形界面和其它特性，并且依赖于engine。后者则是命令行工具客户端docker。
   
   1. Docker Engine is an open source containerization technology for building and containerizing your applications. Docker Engine acts as a client-server application with:
      A server with a long-running daemon process dockerd.
      APIs which specify interfaces that programs can use to talk to and instruct the Docker daemon.
      A command line interface (CLI) client docker.
3. 为了拥有更好的学习效果，并且考虑到Desktop的速度，暂时不安装Docker Desktop。
4. 修改Docker的源，来提升镜像的下载速度。
4. Windows上的安装可以直接使用Desktop版本，主要的问题是各种报错，解决方法可以看手册。

## Docker使用

1. 寻找镜像参数：search
2. 下载拉取镜像：pull
3. 查看本地的Image仓库
4. 运行镜像

- Docker的生命周期：
  - Dockerfile可以自定义构建镜像
  - 镜像下run生成容器
  - docker可以push到Docker仓库，也可以创建私有仓库。
  - 本地也可以保存和管理镜像文件。

## Docker镜像

1. 镜像如何诞生，具体应该怎么使用？
   1. 镜像的生成方式：自己创建、下载拉取镜像、在现有基础上创建新的。
1. 好处之一就在于可以直接在Windows上安装运行Linux上的应用。
1. 怎么制作自己的镜像？
   1. dockerfile制作镜像
      1. 镜像中包含了运行端口、代码位置，可以包含命令行脚本
   1. 目录挂载：三种方式build mount, volume, tmpfs mount
1. hello-world镜像：最小的镜像
   1. 可以看到三行命令from scratch(从头开始构建) COPY hello /（把文件复制到根目录）CMD ["/hello"] 表示容器启动执行命令行。
1. base镜像：
   1. 从零开始的镜像，并且可以在这个镜像基础上进行拓展
   1. 在Linux基础上进行的OS安装都可以以host的kernel为基础进行拓展，通过一个很小的rootfs就可以模拟出多种LinuxOS。当然，这种模拟出的镜像不能够更改内核版本。
   1. 