---
layout: post
title: "tkinter relief应用"
date: 2025-07-06
description: "如何设置relief参数"
tag: python
---  
在python编程过程中我们经常会遇到需要图形界面的情况，在tkinter中有一个参数relief用它来定义控件边框的样式。relief有6个值，可以设定 flat、sunken、raised、groove、ridge、solid，默认为 flat。
那这个参数设定完是什么结果呢？我编写了一段例程，来显示加载各relief的参数的效果。

### 例程：
    ···
    import tkinter as tk

    N=0
    def button_01_click():
        global N
        if N<6:
            frame1 = tk.Frame(win, width=300, height=200, bd=3, relief=reliefs[N], bg='lightyellow')
            frame1.place(x=50, y=150)
            string = f'当前边框是：{reliefs[N]}模式'
            label_02_text = tk.StringVar()
            label_02_text.set(string)
            label_02 = tk.Label(win, textvariable=label_02_text,width=25, font=f'楷体,16')  # relief=reliefs[1]
            label_02.place(x=50, y=50)
            N=N+1
        else:
            N=0
    
    win= tk.Tk()  # 创建窗口
    win.geometry('400x420') # 创建400*300的窗口
    win.title('relief设置例程')
    win.attributes("-topmost", True)  # 置顶
    
    reliefs=['flat','sunken','raised','groove','ridge','solid']
    
    frame1=tk.Frame(win,width=300,height=200,bd=3,relief=reliefs[1],bg='lightyellow')
    frame1.place(x=50,y=150)
    string=f'当前边框是：{reliefs[1]}模式'
    label_02_text = tk.StringVar()
    label_02_text.set(string)
    label_02 = tk.Label(win, textvariable=label_02_text, font=f'楷体,16') # relief=reliefs[1]
    label_02.place(x=50, y=50)
    
    button_01 = tk.Button(win, text="切换边框模式", command=button_01_click,bg='whitesmoke',width=15,bd=3,fg="black",font="楷体 17")
    button_01.place(x=100,y=360)
    
    win.mainloop()

    ···    

### 运行结果：  
1.flat 
![image](https://github.com/user-attachments/assets/6a39f780-43b1-4d3a-ab29-0f4e337cf61b)


2.sunken
![image](https://github.com/user-attachments/assets/1b3c2f3b-ae72-4515-9fd1-49657e54141f)

3.raised
![image](https://github.com/user-attachments/assets/e7f90b76-a821-4ecf-8deb-d6797c6cbb02)

4.groove
![image](https://github.com/user-attachments/assets/c76f78c6-de80-47ab-9621-49f6f10e4774)

5.ridge
![image](https://github.com/user-attachments/assets/6c748508-3d3d-449f-a3ad-b800e75ea60f)

6.solid
![image](https://github.com/user-attachments/assets/7394900a-bb3c-44e8-b7f4-a7bbb386405d)

以上是relief参数的设置和效果情况，编程时可参考。






