---
layout: post
title: "tkinter RadioButton用法"
date: 2025-07-06
description: "如何设置RadioButton"
tag: python
---  
在这里我们简单介绍一下tkinter Radio Button的基本用法。在tkinter中，Radiobutton组件用于创建单选按钮，允许用户从一组互斥的选项中选择一个。要使用Radiobutton，你需要指定一个variable和一个value。variable是一个IntVar或StringVar，用于存储当前选中的单选按钮的值。value是每个Radiobutton关联的值，当用户点击该按钮时，variable的值会被设置为value。

### 以下是如何使用Radiobutton的步骤和示例代码：
1. 创建Radiobutton组件:
使用`Radiobutton(parent, text="选项文本", variable=variable, value=some_value)`来创建每个单选按钮。
parent参数指定了Radiobutton所属的父容器（例如窗口或Frame）。
text参数指定了按钮上显示的文本。
variable参数指定了与按钮关联的IntVar或StringVar变量。
value参数指定了当用户选择此按钮时，variable应该被设置为的值。
2. 设置variable:
使用`IntVar()或StringVar()`创建一个变量，用于存储用户选择的单选按钮的值。
`IntVar()`用于存储整数值，`StringVar()`用于存储字符串值。
在创建Radiobutton时，将variable参数设置为此变量。
3. 指定每个按钮的value:
为每个单选按钮设置不同的value，以便在用户选择时区分它们。
例如，可以为第一个按钮设置value=1，第二个按钮设置value=2，依此类推。
4. 将Radiobutton添加到容器中:
使用pack()，grid()或place()方法将Radiobutton添加到窗口或Frame中。
5. 处理选择事件(可选):
可以使用command参数在用户选择单选按钮时执行一个函数。
在函数中，可以获取variable的值来确定用户选择了哪个选项。

### 代码
    import tkinter as tk

    def on_radio_button_change():
        """当单选按钮状态改变时调用的函数。"""
        selected_value = var.get()
        print('selected_value=',selected_value)
        label.config(text=f"你选择了：{selected_value}")
    
    root = tk.Tk()
    root.title("RadioButton示例") # 设置窗口抬头
    img = tk.PhotoImage (file="E:\OneDrive\照片\图标\\trade.png")  # 设置图标路径
    root.iconphoto(False,img)           # 设置窗口图标
    root.geometry("300x300+900+150")    # 设置窗口及位置
    root.config(bg='lightgray')         # 设置背景色
    root.attributes("-topmost",True)    # 置顶
    
    var = tk.IntVar(value=0)  # 使用StringVar来存储RadioButton的值
    
    radio_button1 = tk.Radiobutton(root, text="选项1", variable=var, value=1,font='楷体 16', command=on_radio_button_change)
    radio_button1.place(x=50,y=50)
    
    radio_button2 = tk.Radiobutton(root, text="选项2", variable=var, value=2, font='楷体 16',command=on_radio_button_change)
    radio_button2.place(x=50,y=100)
    
    radio_button3 = tk.Radiobutton(root, text="选项3", variable=var, value=3,font='楷体 16', command=on_radio_button_change)
    radio_button3.place(x=50,y=150)
    
    label = tk.Label(root, text="点击选择RadioButton",font='楷体 16',bg='lightgray')
    label.place(x=50,y=200)
    
    root.mainloop()
### 运行结果

![img.png](img.png)

![img_1.png](img_1.png)
