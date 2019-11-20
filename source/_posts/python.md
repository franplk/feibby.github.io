---
title: Python环境安装
date: 2019-11-08 17:50:51
tags:
- Python
categories:
- 环境安装
---



本文介绍了Python环境的安装， 以及依赖包的在线和离线状态下的下载与更新。同时对虚拟环境的开启做了简单介绍。

<!-- more -->

> 1. 下载Python二进制文件
>
>    ```
>    下载地址：https://www.python.org/ftp/python/3.7.4/Python-3.7.4.tgz
>    linux系统下载: wget https://www.python.org/ftp/python/3.7.4/Python-3.7.4.tgz
>    ```
>
> 2. 将二进制文件上传到要安装服务器
>
>    ```
>    SSH软件上传
>    ```
>
> 3. 安装--以下步骤都在要安装的服务器上操作
>
>    ```
>    1. tar -zxvf Python-3.7.4.tgz # 解压安装包
>    2. cd ./Python-3.7.4  # 进入解压后的目录
>    3. ./configure --prefix=/usr/local/my_python_path #初始配置，--prefix指定安装目录
>    4. make && make install  # 编译源码 + 程序安装
>    ```
>
> 4. 安装完成，配置环境
>
>    ```
>    1. 建立软连接到系统环境变量
>    	ln -s /usr/local/my_python_path/bin/python3 /usr/bin/python3 
>    2. pip 建立
>    	ln -s /usr/local/my_python_path/bin/pip3 /usr/bin/pip3
>    ```
>    
> 5.  测试是否安装成功
>
>    ```
>    1. python3 -V # 验证python3
>    2. pip3 -V # 验证pip
>    ```
>    
> 6.  更新pip(非必须)
>
>    ```
>    # python自带pip可能不是最新，可以更新
>    pip3 install --upgrade pip
>    ```
>

### 开启虚拟环境(非必须)

> 虚拟环境是指针对部署项目的一个单独的python环境（依赖包归该虚拟环境所有），其他项目的依赖不会对其产生影响。
>
> 虚拟环境不是必须的，只有在多个python项目运行，且互相依赖的相同依赖包版本不一致时，才是必须的。
>
> 1. 初始化虚拟环境
>
>    ```
>    # 进入想要生成虚拟环境的目录下 比如 ~/apps/model
>    # 其中第一个venv是python生成虚拟环境的命令
>    # 第二个venv是虚拟环境存放的目录，可以修改成其他名字，比如venv-model
>    python3 -m venv venv
>    python3 -m venv venv-model
>    ```
>
> 2. 激活虚拟环境
>
>    ```
>    # 激活虚拟环境--linux系统
>    source venv/bin/activate
>    # 激活虚拟环境--windows系统
>    venv/Scripts/activate.bat
>    ```
>
> 3. 退出虚拟环境
>
>    ```
>    # 在当前虚拟环境下，运行
>    deactivate
>    ```
>
> 虚拟环境生成后，就是一个python的运行环境，操作与在系统中一样。

### 依赖包安装

------

如果是在虚拟环境中运行项目，请激活虚拟环境后，在虚拟环境下操作，反之在当前系统下操作即可。

#### 在线安装

> ```
>  # 安装依赖包 -r 指定依赖文件
> 1. pip3 install -r requirements.txt
> ```

#### 离线安装

> 1. 备份依赖包---可上网的开发环境
>
>    ```
>    # 备份依赖关系
>    1. pip3 freeze > requirement.txt
>    # 在线下载依赖包到指定目录
>    2. pip3 download -d pack_directory -r requirements.txt
>    	-d 指定依赖包保存目录
>    	-r 指定依赖包汇总文件
>    ```
>
> 2. 还原依赖包---离线服务器
>
>    ```
>    # 安装依赖包
>    1. pip3 install --no-index --find-links=pack_directory -r requirements.txt
>     --no-index 禁止去网络下载
>     --find-links 指定去哪里寻找安装包，这里是安装包文件夹
>     -r 指定依赖包文件
>    ```
>

