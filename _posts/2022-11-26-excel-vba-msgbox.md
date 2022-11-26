---
layout: post
title: "Excel VBA Msgbox用法"
date: 2022-11-26
description: "Excel VBA Msgbox"
tag: VBA
---
在Excel VBA 使用过程中我们经常要用到使用"Msgbox"的时候，也可以说掌握"Msgbox"使用方法，在学习VBA过程中是必不可少的。
## Msgbox 语法格式
MsgBox (prompt, [ buttons, ] [ title, ] [ helpfile, context ])

prompt：我们要显示的信息，字符格式，可以多行显示。
bottons：可选，对话框中的按钮或图标显示的类型或方式。
title：对话框的名称，默认情况下为程序名，如“Microsoft Excel”。
helpfile和context不常用不做介绍。

### 1.简单显示信息
    Sub msgbox_test1()

        MsgBox "Hello world!"
    End Sub
    
运行结果如下：

![image](https://user-images.githubusercontent.com/70909689/204091323-06e04082-ccf0-4393-b949-182cf0e51bbf.png)

图片中的“Microsoft Excel”即命令中省略的“title”

图片中的“Hello world！”为命令中的prompt

图片中的“确定”按钮为命中中省略的buttons

![image](https://user-images.githubusercontent.com/70909689/204091558-7f612bb3-7806-46f2-a7aa-c4b6c9933474.png)

### 2.设置msgbox的title

    Sub msgbox_test2()
        MsgBox "Hello world!", , "My Title"
    End Sub
显示结果如下：

![image](https://user-images.githubusercontent.com/70909689/204091992-7dbd8bf1-1c47-4d11-9f56-32142b278ed7.png)

### 3.

