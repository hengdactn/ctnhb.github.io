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

### 3.设置“buttons”
    Sub msgbox_test3()
         MsgBox "Hello world!", vbInformation, "My Title"
    End Sub

![image](https://user-images.githubusercontent.com/70909689/204092384-7ebd33f0-e6bd-490c-a360-c74a4b2e1206.png)

### 4.设置显示“确认”和“取消”两个按钮

    Sub msgbox_test4()
        mychoice = MsgBox("程序继续运行请安确定键，否则按取消键!", vbInformation + vbOKCancel, "我的程序")
        MsgBox "你按下了 " & mychoice & " 按钮", vbInformation, "按键检测"
    End Sub
    
运行结果如下下：

![image](https://user-images.githubusercontent.com/70909689/204093472-cea9e7d5-4139-4abe-a48e-ef8642a7ef8c.png)

当我们按下“确认”按钮的时

![image](https://user-images.githubusercontent.com/70909689/204093706-57d2d4ea-fe14-41a4-b762-4dc7f4a2b104.png)

当我们按下“取消”按钮时

![image](https://user-images.githubusercontent.com/70909689/204093734-73ce256e-1580-45bc-990e-c563e9252c0d.png)

### 常用的buttons的值

Constant	      Value	Description

vbOKOnly	        0	Display OK button only.

vbOKCancel	        1	Display OK and Cancel buttons.

vbAbortRetryIgnore	2	Display Abort, Retry, and Ignore buttons.

vbYesNoCancel	    3	Display Yes, No, and Cancel buttons.

vbYesNo	            4	Display Yes and No buttons.

vbRetryCancel	    5	Display Retry and Cancel buttons.

vbCritical	        16	Display Critical Message icon.

vbQuestion	        32	Display Warning Query icon.

vbExclamation	    48	Display Warning Message icon.

vbInformation	    64	Display Information Message icon.

## 以上就是Msgbox的基本用法，欢迎联系[ctnhb@126.com](mailto:ctnhb@126.com)


    
