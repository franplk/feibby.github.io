---
title: pyinstaller程序打包与发布
date: 2019-11-11 09:36:27
tags: Python
---



该文档说明了如何使用 pyinstaller 将应用打包成可执行的exe文件

<!-- more -->

### Pyinstaller安装

> 1. 使用pip进行安装
>
>    ```
>    # 安装
>    $ pip install pyinstaller
>    ```
>
> 2. 几个命令介绍
>   | 命令选项 | 命令说明                                                    |
>    | :------: | :---------------------------------------------------------- |
>    |    -F    | 打包成单个exe文件                                           |
>    |    -D    | 打包成文件形式。Flask项目因为有非python文件，需要使用该选项 |
>    |    -i    | 指定打包后应用程序的图标 --- ico文件                        |
>    |    -w    | 指定对于Qt桌面程序，不显示Dos窗口                           |
>    |    -d    | 编译为debug模式，用于测试时获取日志信息                     |

### 应用程序打包

> 1. 打包成EXE
>
>    ```
>    #在项目根目录下，执行打包命令
>    $ pyinstaller -D -w code/run.py
>    
>    # 如果已有 .spec 文件，可以执行以下命令打包
>    $ pyinstaller run.spec
>    ```
>
> 2. 找到可执行文件目录
>
>    ```
>    2.1 打包完成后，生成一个dist目录，下面有一个run文件夹。run文件夹下面包含了可执行文件以及所有的项目依赖文件。
>    2.2 对于Flask项目，在运行前需要将resources目录复制到该文件夹下面
>    ```
>
> 3. 运行/发布
>
>    ```
>    运行 run.exe即可
>    ```

### 制作程序安装包

> 制作成安装包需要使用 Inno SetUp 软件。
>
> 1. 安装 InnoSetUp
>
>    ```
>    下载安装 inno setup （下载地址：http://www.jrsoftware.org/isdl.php）
>    ```
>
> 2. 启动 InnoSetUp 新建项目即可根据步骤完成
>
> 3. 制作完成后，可以进行正常发布

### 出现问题以及解决

> 1. pyinstaller与PyQt版本兼容问题
>
> ```
> 原因：pyinstaller要与PyQt5的版本对应
> 
> 解决方案：目前已测试 pyinstaller 3.5 需要使用 PyQt5==5.13.1 版本。
> 其他具体兼容性需要去官网查询
> ```
>
> 2. sklearn等机器学习包不能打包
>
> ```
> 原因：该问题是因为机器学习包等用到了大量的C++库。这些文件是c/c++编译成的python库，供python调用，需要额外处理。
> 
> 解决方案：将这些库添加到 spec文件的 hiddenimports 属性中。
> hiddenimports=['cython','sklearn','sklearn.utils._cython_blas',
>     'sklearn.neighbors.typedefs',
>     'sklearn.neighbors.quad_tree',
>     'sklearn.neighbors.ball_tree',
>     'sklearn.neighbors.dist_metrics',
>     'sklearn.neighbors.kd_tree',
>     'sklearn.tree._utils',
>     'sklearn.tree._criterion',
>     'sklearn.tree._splitter',
>     'sklearn.tree._utils'
> ],
> 
> 参考链接：[https://bbs.testerhome.com/articles/19886]
> ```
>
> 3. pyecharts 不兼容
>
> ```
> 描述：使用pyinstaller进行python程序打包的时候，对pyecharts是不兼容的，因此不能将pyecharts打包到程序当中。
> 
> 原因：pyecharts涉及到一些js，json文件没有打包，使得整个打包软件找不到相关文件，所以报错。
> 
> 解决：从python的site_package中找到pyecharts文件夹，并把这整个文件夹都放到与exe文件同级的文件夹下面即可
> 
> 参考链接：[https://blog.csdn.net/weixin_43865152/article/details/93781051]
> ```
>
> 4. 打包多进程程序，运行卡死电脑
>
>    ```
>    具体表现：
>    在使用Pyinstaller打包Python程序的时，打包过程正常，但在运行时会出错，表现为进程不断增加至占满电脑CPU死机。
>    
>    原因：
>    因为程序使用了多进程模式，而在windows上Pyinstaller打包不支持多进程程序，需要添加特殊指令。
>    
>    解决方案：
>    在 if __name__=='__main__:'下添加一句
>    	multiprocessing.freeze_support()
>    即可。
>    
>    参考链接：[https://blog.csdn.net/zyc121561/article/details/82941056]
>    ```
>
> 5. 后续补充