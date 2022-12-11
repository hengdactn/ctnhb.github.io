---
layout: post
title: "Excel VBA 的颜色index"
date: 2022-12-11
description: "Excel VBA linefeed enter"
tag: VBA
---
在使用excelvba时，经常会遇到需要设置单元格或区域的颜色，今天我们讨论一下如何使用color index设置颜色。
为了直观我们编一个小程序来显示颜色及数值，方便以后调用。
       Sub color_test()
          Dim i, j, index As Integer
          index = 1
          Range("C3，E3,G3,I3") = "数值"
          Range("D3,F3,H3,J3") = "颜色"
          For i = 3 To 10 Step 2
              For j = 4 To 17
                  Cells(j, i) = index
                  Cells(j, i + 1).Interior.ColorIndex = index
                  index = index + 1
              Next j
          Next i
          Range("C3:J17").BorderAround xlDouble
          Range("C3:J17").Borders(xlInsideHorizontal).linestyle = xlContinuous
          Range("C3:J17").Borders(xlInsideVertical).linestyle = xlContinuous
      End Sub
      
运行结果如下

![image](https://user-images.githubusercontent.com/70909689/206901856-28cc9633-4680-4555-a08a-cd0df8466693.png)

我么可以记下下面的值，方便我们以后调用。欢迎联系[ctnhb@126.com](mailto:ctnhb@126.com)
