---
layout: post
title: "Excel VBA 单元格区域边框处理"
date: 2022-12-11
description: "Excel VBA boders"
tag: VBA
---

在我们处理Excel工作时，经常会遇到需要对excel的单元格或区域进行边框设置的情况。比如添加或者去除边框。下面我们探讨一下如何处理。

### 通过录制宏的方法添加边框
通过录制的宏的的方法添加边框：
1.点击`开发工具`

![image](https://user-images.githubusercontent.com/70909689/206888348-4bdf76d1-d420-4d61-9c64-4f370857a8ee.png)
2.点击录制宏
![image](https://user-images.githubusercontent.com/70909689/206888377-c05d2dc1-85fb-4e96-ab26-9e2fc36d6560.png)
3.选取要添加边框的区域
![image](https://user-images.githubusercontent.com/70909689/206888434-e93ebade-038e-4bba-8efc-f501fac3d6c2.png)

4.选择开始选项卡
![image](https://user-images.githubusercontent.com/70909689/206888477-97eae834-11fe-4d01-9b76-e6a97d9409fa.png)

5.选择边框下拉选框

![image](https://user-images.githubusercontent.com/70909689/206888500-6ddb3146-4f31-4076-8a88-0227725ebee9.png)

6.选择`所有边框线`

![image](https://user-images.githubusercontent.com/70909689/206888615-1ff96356-d5dc-4711-a644-6a250aec5161.png)

7.结果如下

![image](https://user-images.githubusercontent.com/70909689/206888641-0fceedd0-93fb-4161-9b08-d22ee1c64b9f.png)

8.所录制的宏如下
    Sub 宏2()
    '
    ' 宏2 宏
    '

    '
    Range("D6:G7").Select
    Range("G7").Activate
    Selection.Borders(xlDiagonalDown).linestyle = xlNone
    Selection.Borders(xlDiagonalUp).linestyle = xlNone
    With Selection.Borders(xlEdgeLeft)
        .linestyle = xlContinuous
        .ColorIndex = 0
        .TintAndShade = 0
        .Weight = xlThin
    End With
    With Selection.Borders(xlEdgeTop)
        .linestyle = xlContinuous
        .ColorIndex = 0
        .TintAndShade = 0
        .Weight = xlThin
    End With
    With Selection.Borders(xlEdgeBottom)
        .linestyle = xlContinuous
        .ColorIndex = 0
        .TintAndShade = 0
        .Weight = xlThin
    End With
    With Selection.Borders(xlEdgeRight)
        .linestyle = xlContinuous
        .ColorIndex = 0
        .TintAndShade = 0
        .Weight = xlThin
    End With
    With Selection.Borders(xlInsideVertical)
        .linestyle = xlContinuous
        .ColorIndex = 0
        .TintAndShade = 0
        .Weight = xlThin
    End With
    With Selection.Borders(xlInsideHorizontal)
        .linestyle = xlContinuous
        .ColorIndex = 0
        .TintAndShade = 0
        .Weight = xlThin
    End With
    End Sub

可以看到通过录制宏的办法实现起来简单，但是代码复杂。
### 简单添加边框的办法
1.代码如下：
        Sub setborders()
            Dim rng As Range
            Set rng = Range("D6:G7")
            With rng
                .BorderAround xlDouble
                .Borders(xlInsideVertical).linestyle = xlContinuous
                .Borders(xlInsideHorizontal).linestyle = xlContinuous
            End With
        End Sub
2.运行结果如下：

![image](https://user-images.githubusercontent.com/70909689/206889233-5948be46-d395-45a0-9c14-69761a7d39d5.png)

可见第二种方法就简单多了。

### 删除所选区域的边框。
1.代码如下：
    Sub delborders()
      Dim rng As Range
      Set rng = Range("D6:G7")
      rng.Borders.linestyle = xlNone
    End Sub
2.运行结果如下：

![image](https://user-images.githubusercontent.com/70909689/206889450-d4c3bc18-ebfc-49d1-a502-8864e919394a.png)

### 我们可以通过一个程序来练习添加和删除边框
    Sub borders_test()
        setborders
        MsgBox "按确认按钮删除边框！"
        delborders
    End Sub
运行结果如下：

![image](https://user-images.githubusercontent.com/70909689/206889689-54e5f733-7e64-44e0-a159-f91b4f9b9621.png)

    
好，以上就是我么对边框的一些处理，欢迎联系[ctnhb@126.com](mailto:ctnhb@126.com)

