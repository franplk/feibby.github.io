---
title: Docker环境安装
date: 2019-11-09 16:50:51
tags:
  - Docker
categories:
  - 环境安装
cover_picture: /images/avatar.jpg
---

 Docker 是一个开源的应用容器引擎，让开发者可以打包他们的应用以及依赖包到一个可移植的镜像中，然后发布到任何流行的 Linux或Windows 机器上，也可以实现虚拟化。 

<!-- more -->

本文介绍了Docker的简单安装部署，以及几个简单命令操作

### 在线安装

不同的操作系统安装命令不一致

1. centos命令

   ```
   # -y 指定免交互安装
   $ sudo yum –y install docker-ce
   ```

2. ubuntu命令

   ```
   # 安装最新版Docker
   $ sudo apt-get install docker-ce
   ```

### 二进制安装 -- 适用离线

二进制安装方式适合服务器无法连接外网的环境。

1. 准备二进制文件

   ```
   官网下载稳定版，根据操作系统选择适合的版本
   下载地址：https://download.docker.com/linux/static/stable/x86_64/
   ```

2. 解压文件并转移文件

   ```
   # 解压文件
   $ tar –zxf docker-19.03.2.tgz
   # 移动文件
   # 将加压后文件夹的所有内容移动到某个系统环境变量下
   # 比如：/bin, usr/bin，usr/local/bin
   $ sudo cp docker/* /usr/bin/
   ```

3. 启动docker服务

   ```
   # 启动Docker服务
   # & 表示后台运行
   $ sudo dockerd &
   ```

4. 验证安装成功

   ```
   # 方式一：查看docker版本信息
   $ sudo docker version
   # 方式二：查看docker信息
   $ sudo docker info
   ```

### Docker基本操作

1. 应用启动

   ```
   # 创建新容器---交互模式
   # 该方式用于改造镜像，生成新镜像（Dockerfile操作）
   $ docker run -it image_id /bin/bash
   
   # 创建新容器 --- 后台运行
   # 用于启动新的应用
   # -d 指定daemon模式
   # -p 指定映射端口
   # --name 指定新创建的容器的名称
   $ docker run -d -p po:pi --name c_name image_id
   ```

2. 应用查看

   ```
   # 查看运行中的容器 -a 表示所有容器，包括停止的容器
   $ docker ps -a
   
   # 交互模式进入容器，可以做一些操作，比如查看日志等
   # container_id 容器的ID
   # command 进入后执行的命令，一般设置为 /bin/bash
   $ docker exec container_id command
   ```

3. 应用停止/恢复

   ```
   # 应用停止
   # -t 指定等待多长时间(单位：s)后推出
   $ sudo docker stop -t 60 container_id
   
   # 应用恢复
   $ sudo docker restart container_id
   ```

   