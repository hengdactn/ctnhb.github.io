---
layout: post
title: "Windows设置程序开机启动"
date: 2022-11-25
description: "开机启动"
tag: Windows
---  
在设置“alist"网络硬盘列表程序使用的过程中涉及到要把程序设置为`开机启动`，Windows怎样设置程序`开机启动`呢？我们以设置start alist.vbs为例来设置其自启动，我的操作系统是Win10 家庭中文版，具体操作如下。
### 打开资源管理器，并定位到要设置自启动的程序
![Ashampoo_Snap_2022年11月25日_12h19m04s_001_alcloud](https://user-images.githubusercontent.com/70909689/203900585-0b025af3-9608-4ca6-898f-3994d6d17c32.png)

### 创建快捷方式
![Ashampoo_Snap_2022年11月25日_12h23m39s_003_](https://user-images.githubusercontent.com/70909689/203901379-89fdfd71-b1c3-4a91-b504-6f9c8ab1686f.png)

这时文件夹内会多出一个文件
![Ashampoo_Snap_2022年11月25日_12h28m04s_004_alcloud](https://user-images.githubusercontent.com/70909689/203901380-d7a9bf1c-5e7a-47b1-9891-f968fd30b0fd.png)

复制这个快捷方式
### 打开`启动`菜单添加启动项
同时按“win”+“R”键，输入shell:Common Startup
![Ashampoo_Snap_2022年11月25日_12h44m11s_008_运行](https://user-images.githubusercontent.com/70909689/203902975-9e5ec514-0c75-48cc-8a51-a7a77f70fa09.png)

这时电脑会打开启动程序窗口
![Ashampoo_Snap_2022年11月25日_12h38m03s_007_启动](https://user-images.githubusercontent.com/70909689/203902396-83a23b80-4fd0-4f48-8de4-ce4b08a3ea49.png)

粘贴复制的快捷方式
![Ashampoo_Snap_2022年11月25日_12h35m27s_006_启动](https://user-images.githubusercontent.com/70909689/203902406-4f1212e9-b39e-4816-ac76-41bb47bd0ea8.png)


重启电脑设置生效。
