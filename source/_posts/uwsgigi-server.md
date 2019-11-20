---
title: uwsgi服务安装
date: 2019-11-08 20:50:51
tags:
- UWSGI
categories:
- 环境安装
---

uwsgi是linux操作系统中，通过python编写的支持wsgi规范的python web服务器，。支持Flask/Django等编写的web程序，常用与Flask应用的生产部署。

<!-- more -->

### pip安装

1. 安装 python 提供的最新版 uwsgi

   ```
   # 系统级安装--非虚拟环境下安装
   pip install uwsgi
   ```

2. 制作软连接

   ```
   # uwsgi连接到环境变量，便于直接使用
   # uwsgi_path：uwsgi的安装路径 一般为 python_home/site-packages/uwsgi
   ln -s /uwsgi_path/uwsgi /usr/local/bin
   ```

### 二进制安装--适合离线

1. uwsgi二进制文件准备

   方式：网络下载最新版本

   ```
下载地址：http://projects.unbit.it/downloads/uwsgi-latest.tar.gz
   
   linux系统下载: wget http://projects.unbit.it/downloads/uwsgi-latest.tar.gz
   ```
   
2. 文件解压编译安装

   ```
   # 解压安装包
   $ tar zxvf uwsgi-latest.tar.gz
   # 重命名为uwsgi(非必须)
   $ mv uwsgi-latest/ uwsgi
   # 进入uwsgi目录，编译安装
   $ cd uwsgi
   $ make
   ```

3. 制作软连接

   ```
   # uwsgi连接到环境变量，便于直接使用
   # 执行目录为当前uwsgi目录
   ln -s ./uwsgi /usr/local/bin
   ```

### uwsgi应用操作

1. 应用启动

   ```
   # --ini 指定 uwsgi 配置文件路径
   uwsgi --ini uwsgi.ini
   ```

2. 应用重启

   ```
   # --reload指定模式为重启
   # uwsgi.pid 为 uwsgi应用的pid进程ID存储文件
   # 该文件在 uwsgi.ini 中配置
   uwsgi --reload uwsgi.pid
   ```

3. 关闭应用

   ```
   # --reload指定模式为重启
   # uwsgi.pid 为 uwsgi应用的pid进程ID存储文件
   # 该文件在 uwsgi.ini 中配置
   uwsgi --stop uwsgi.pid
   ```

