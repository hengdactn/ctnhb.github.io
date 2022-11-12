---
layout: post
title: "使用VBA代码加载“引用"”
date: 2022-11-12
description: "VBA referance"
tag: VBA
---   
我们在进行VBA编程的时偶尔会需要添加引用，那么如何用代码添加引用呢下面我们来探讨一下。
## 首先查看一下我们都使用了那些引用
### 打开VBA选择选择`工具`菜单

![referance1](https://user-images.githubusercontent.com/70909689/201476860-789228e0-7b4a-42dd-903f-30da5821f455.jpg)

### 选择`引用`菜单

![referance2](https://user-images.githubusercontent.com/70909689/201476952-5c7b9dde-379a-421b-9a62-45e037323851.jpg)

### 查看引用项目

![referance3](https://user-images.githubusercontent.com/70909689/201477000-3da65f61-aa1f-4f54-a369-8830505d9b9b.jpg)

我们发现有四个引用项。

## 用代码查看我们的引用项

运行下面代码

Private Sub Vba_referance()
  '遍历所有已使用的引用
  Dim i As Integer                
    i = 2                
    With Sheet1              
      For Each refed In ThisWorkbook.VBProject.References
        .Cells(i, 1) = refed.Name
        .Cells(i, 2) = refed.GUID
        .Cells(i, 3) = refed.Major
        .Cells(i, 4) = refed.Minor
        i = i + 1
      Next
   End With
End Sub

会在sheet1页面上列出我们的引用项

![referance5](https://user-images.githubusercontent.com/70909689/201477443-bd012dfb-616c-440b-90b4-de7d2b773118.jpg)

可以看出这些项和我们的引用项是一一对应的。
## 查询要引用项的代码

### 选择我们需要的引用
以selenium 引用为例

![referance6](https://user-images.githubusercontent.com/70909689/201477726-b01cc55c-087e-4045-ac63-7a0232c29441.jpg)

选择并确认。

### 运行该才的代码

![referance7](https://user-images.githubusercontent.com/70909689/201477868-1323b97b-16e2-4658-be43-7af9005fe866.jpg)

我们发现现在比以前增加了一项`Selenium`引用项。
这就是我们想要引用的`Selenium`的相关参数。

### 取消`Selenium Type Library`引用。
去掉对`Selenium Type Library`对勾，取消对`Selenium Type Library`的引用并确认。

## 运行代码加载引用


### 运行一下代码
Sub AddSeleniumReferance()
    On Error Resume Next
    Dim oRef
    Set oRef = ThisWorkbook.VBProject.References.AddFromGuid("{0277FC34-FD1B-4616-BB19-A9AABCAF2A70}", 2, 0)
End Sub

{0277FC34-FD1B-4616-BB19-A9AABCAF2A70}，2，0为我们刚查询到的参数。

### 查看运行结果
![referance8](https://user-images.githubusercontent.com/70909689/201478545-c4718fd1-ed1e-4772-a77d-c68d079097b0.jpg)


以上就是用代码实现对引用的加载，欢迎交流 [ctnhb@126.com](mail to:ctnhb@126.com)



