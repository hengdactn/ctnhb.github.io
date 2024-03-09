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
mport tkinter as tk
from tkinter.messagebox import *

title='警告'
message='这是一个警告信息框'

win=tk.Tk()
win.withdraw()

result=showwarning(title,message)
print('result=',result)
```
运行以上代码会显示：  

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/77d143ae-861f-4153-9345-817927278771)  

当我们点击确定，则result= ok。  

### 3.错误信息框  
创建和显示一个具有指定标题和消息的错误消息框。  

```
import tkinter as tk
from tkinter.messagebox import *

title='错误'
message='这是一个错误信息框'

win=tk.Tk()
win.withdraw()

result=showerror(title,message)
print('result=',result)
```

运行以上代码会显示：  

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/026aab30-3bca-4573-8c1c-e6b950d3ea64)  


当我们点击确定，则result= ok。 

### 4.疑问消息框  
提出一个问题。 在默认情况下显示 YES 和 NO 按钮。 返回所选择按钮的符号名称。  
```
import tkinter as tk
from tkinter.messagebox import *

title='是（y）|否（n）？'
message='这是一个疑问信息框，请选择是或否。'

win=tk.Tk()
win.withdraw()

result=askquestion(title,message)
print('result=',result)
```
运行以上代码会显示：  

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/33adb588-cd20-4e03-9b9e-df46b623b4b9)


当我们点击"是"，则result= yes；当我们点击“否”，则result=no。








