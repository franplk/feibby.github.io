---
title: hexo_blog
date: 2019-11-12 16:30:04
tags: Hexo
categories: 博客搭建
---





本文分享一篇博客搭建文章，介绍了如何使用Hexo博客框架搭建个人博客。



### Github配置

1. Github账号

   首先，需要自己有一个Github账号，没有的话去GIthub官网注册一个即可。

   搭建博客需要一个域名（无需自己申请），GitHub 为我们提供了的GitHub Pages 功能，自动为我们提供一个以Github用户名为前缀的域名：{username}.github.io。 

   

2. 设置GitHub SSH key

   设置GIthub SSH key是为了在站点部署代码时，可以通过Hexo命令直接提交代码。如果不设置SSH Key，后期也可以使用"Https"方式的 git 仓库地址，不过该方式会弹出输入用户名和密码的界面。该方式适合在windos下的部署，在linux下会有问题。

   

3. 创建仓库作为我们的站点代码库

   在Github上创建一个仓库，仓库的名称必须为：{username}.github.io。比如你的Github账号为apple，则新建的仓库名称为：apple.github.io. 

   

###  环境准备

1. 安装NodeJS

   首先在个人电脑上安装NodeJS，下载地址为： [ NodeJs下载地址](https://nodejs.org/zh-cn/download/)

   安装完毕后，验证一下 npm 命令是否可以使用，以确保NodeJS安装成功。

2. 安装Hexo

   NodeJS安装完成后，通过npm命令进行 Hexo的安装。Hexo是一个博客框架，帮助我们快速搭建个人博客，Hexo为我们提供一个NodeJS的客户端命令行工具，用于Hexo项目的创建，页面新建，代码编译以及部署等功能。执行以下命令进行安装：

   ```
   # -g 选项指定全局安装
   $ npm install -g hexo-cli
   ```



### 博客项目搭建

1. 初始化项目

   进入到项目创建目录（比如，E:\develop）执行以下命令，初始化项目：

   ```
   # 其中blog_name是博客名称，需要设定
   $ hexo init {blog_name}
   ```

   比如我的博客名称为 "myblog"，可以执行以下命令来初始化项目：

   ```
   hexo init myblog
   ```

   此时，会在当前目录下面生成myblog文件夹，该文件夹下面包含以下文件：

   - myblog
     - scaffolds : 生成博客文章的模板文件目录
     - source : 博客源码目录
     - themes：主题目录，后期下载的主题都可以放在该目录下
       - landscape 主题，Hexo默认提供的主题
     - _config.yml ：博客配置文件

   这样一个初始化的博客已经建立完成，默认提供了一篇文章，后面先发布成功后，再添加个人的文章。

2. 代码编译

   执行以下命令：

   ```
   $ hexo generate
   ```

   或者简写为如下命令：

   ```
   $ hexo g
   ```

3. 启动服务

   编译完成后，本地可以启动以下，测试是否可以访问：

   ```
   $ hexo serve
   ```

   执行以上命令，可以启动服务：

   ```
   $ hexo serve
   INFO  Start processing
   INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
   ```

### 部署到Github

测试可以访问后，可以发布到github.

1. 配置发布地址
2. 执行发布命令