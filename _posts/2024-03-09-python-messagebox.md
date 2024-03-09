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
```
import tkinter as tk
from tkinter.messagebox import *

title='提示'
message='这是一个信息框'

win=tk.Tk()
win.withdraw()

result=showinfo(title,message)
print('result=',result)
```
运行以上代码会显示：  
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/5f521104-5b90-45ee-b26f-54d6b4831ff1)  
当我们点击确定，则result= ok。  
### 2.警告消息框  
创建并显示一个具有指定标题和消息的警告消息框。 

```

```



