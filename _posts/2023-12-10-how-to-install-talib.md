---
layout: post
title: "python如何安装talib"
date: 2023-12-10
description: "python如何安装talib"
tag: python_okx
--- 

因为量化计算的需要，我需要安装talib程序包，但是通过pip install ta-lib安装在过程中报错，怎么也装不上，于是开始寻找正确安装talib的方法，经过不懈努力终于找打了安装不成的原因。主要原因是我们目前使用的操作系统基本都是64位操作系统，而python库中的talib是32位的，所以我们会安装不成功。要想安装成功我们需要用到64位的安装包，但是pip安装源中并不提供，所以我们需要手动下载64位安装包，然后手动安装。  
### 一、talib的下载地址：  
[https://www.lfd.uci.edu/~gohlke/pythonlibs/](https://www.lfd.uci.edu/~gohlke/pythonlibs/)  

找到与我们的python版本想适应的安装包，例如我的python版本是3.79，则需要下载TA_Lib-0.4.24-cp37-cp37m-win_amd64 .whl这个文件。
### 二、手动安装：
在命令行模式进入刚下载文件所在的目录，然后运行pip install TA_Lib-0.4.24-cp37-cp37m-win_amd64 .whl。或不进入下载目录，直接使用路径进行安装 匹配、
install e:\TA_Lib-0.4.24-cp37-cp37m-win_amd64 .whl进行安装。


安装成功后会提示“ Successfully installed TA-Lib ”，这样就可使用了。