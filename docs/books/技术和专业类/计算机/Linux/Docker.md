# Docker技术

## 导论

- 容器技术是一种虚拟化的技术，可以裁剪计算机的资源，充分利用资源去满足需要的应用。
- Docker是容器技术的代表，容器技术是Linux下的一种手段。它对操作系统进程进行了封装隔离，节约了服务器的资源。
- 通过Docker容器技术，可以简化开发流程：本地程序，开发好DockerFile脚本，将代码和环境依赖打包成为镜像文件，其它机器（测试、生产服务器）可以直接运行（docker run）这个镜像，不再需要各种配置。
- Docker基础组件：CLI客户端命令行、API、服务器端。
  - 命令行CLI：Clinet主要需要管理的
- docker核心组件包括了：镜像、容器、网络、数据卷（存储）
  - image: 应用程序所需要的环境，打包为image文件——可以下载，可以自己按照规范写；镜像是一个对象基类，一个模板，用户通过这个对象构建
  - Container:容器，应用程序跑在容器中
  - 镜像仓库（dockerhub就是官方的镜像仓库）:存放镜像文件的仓库。
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

## Docker镜像的原理

1. 镜像如何诞生，具体应该怎么使用？