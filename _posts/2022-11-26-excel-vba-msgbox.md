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

### 5.Msgbox的返回值

Msgbox函数的返回值：
![image](https://user-images.githubusercontent.com/70909689/204094942-8e3b4be8-c4ed-47e9-82ae-ded615c92bde.png)


### 6.常用的buttons的值
buttons的取值表
![image](https://user-images.githubusercontent.com/70909689/204095171-07786b87-1a04-4fba-8d12-16ce47bc74bc.png)

#### 1（.0~5）对话框中按钮的数量和类型

![image](https://user-images.githubusercontent.com/70909689/204095285-6b012fae-08d2-400e-a28c-10372240683f.png)

#### 2.（16，32，48，64）决定对话框中显示的图标

![image](https://user-images.githubusercontent.com/70909689/204095333-88a97438-56c7-486b-8909-7176b1faeadb.png)

#### 3.（0，256，512，768）绝对对话框中默认的活动按钮

![image](https://user-images.githubusercontent.com/70909689/204095369-80d5dbf9-77e6-4dd5-a5ef-beefa15b2c19.png)

#### 4.（0，4096）决定消息框的强制响应性，不常用

![image](https://user-images.githubusercontent.com/70909689/204095396-df431bba-f69c-42fb-8b44-7ac5a2a93639.png)

## 以上就是Msgbox的基本用法，欢迎探讨联系[ctnhb@126.com](mailto:ctnhb@126.com)


    
