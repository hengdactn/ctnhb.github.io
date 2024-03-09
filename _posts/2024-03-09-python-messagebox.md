---
layout: post
title: "python提示框应用"
date: 2024-03-09
description: "如何设置提示框"
tag: python
---  
在python编程过程中我们经常会遇到，要有一些提示信息、警示信息或是确认信息等，那么怎样实现在python中显示这些信息呢，下面我们一块进行讨论：
首先，需要加载一下模块。  
```
    import tkinter  
    from tkinter.messagebox import *      
```
### 1.信息消息框  
创建并显示一个具有指定标题和消息的信息消息框。  
