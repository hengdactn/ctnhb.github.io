---
layout: post
title: "Excel VBA实现对文件的选择"
date: 2022-11-21
description: "excel select files"
tag: VBA
---

 在exce VBA编程的过程中偶尔会用到外部文件，下面我们通过excel VBA编程来实现对文件的选择。我们以在excel工作表中插入图片为例来说明如何操作。

### 格式化待出入图片的单元格

假设我们要在某工作表的“A21”和“B21”单元格插入图片，我们把列宽设置为40，行高设置为145。

    Columns("A:A").ColumnWidth = 40
    Columns("B:B").ColumnWidth = 40
    Rows("21:21").Select
    Selection.RowHeight = 145
    
调整完毕后如下图
![2022 11 21_19h55m05s_001](https://user-images.githubusercontent.com/70909689/203059125-45a9bc36-5ce1-41d0-bd47-2659767bc2b4.jpg)


### 使用Application.FileDialog（）语句选择插入图片

    Dim path As String
    Dim Fobj As FileDialog
    Set Fobj = Application.FileDialog(msoFileDialogFilePicker)
    With Fobj
        .Title = "选择法人身份证正面"
        .AllowMultiSelect = False
        .InitialFileName = ThisWorkbook.path & "\" & ThisWorkbook.Sheets("新建项目").Range("B2") & "\" & ThisWorkbook.Sheets("新建项目").Range("B4")
        .Show
        path = .SelectedItems(1)
    End With
    Range("A21").Select
    ActiveSheet.Pictures.Insert(path).Select
    Selection.ShapeRange.LockAspectRatio = msoFalse
    Selection.ShapeRange.Height = 140
    Selection.ShapeRange.Width = 219
    
    Set Fobj = Application.FileDialog(msoFileDialogFilePicker)
    With Fobj
        .Title = "选择法人身份证背面"
        .AllowMultiSelect = False
        .InitialFileName = ThisWorkbook.path & "\" & ThisWorkbook.Sheets("新建项目").Range("B2") & "\" & ThisWorkbook.Sheets("新建项目").Range("B4")
        .Show
        path = .SelectedItems(1)
    End With
    Range("B21").Select
    ActiveSheet.Pictures.Insert(path).Select
    Selection.ShapeRange.LockAspectRatio = msoFalse
    Selection.ShapeRange.Height = 140
    Selection.ShapeRange.Width = 219   
    
运行结果如下图
![2022 11 21_20h26m51s_004](https://user-images.githubusercontent.com/70909689/203059257-5bd9c0da-e0b8-4d81-9fac-9a70f766cf69.jpg)

### 小结
选择文件我们使用msoFileDialogFilePicker这个参数，即Application.FileDialog(msoFileDialogFilePicker)。

title是文件选择器的标题 

InitialFileName是默认打开的路径

Show是显示选择对话框

SelectedItems(1) 获取选择到的项，为数组，起始为1
![2022 11 21_20h22m18s_003](https://user-images.githubusercontent.com/70909689/203061147-766e8225-e7c8-4a82-af97-0ca8dc3b975a.jpg)

   
    
    
    
