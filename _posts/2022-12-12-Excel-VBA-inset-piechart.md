---
layout: post
title: "VBA在excel工作表中插入饼图"
date: 2022-12-12
description: "VBA在excel工作表中插入饼图"
tag: VBA
---

在使用VBA的过程中，我们会遇到在excel表格中插入图表的情况，今天我们以在工作表中插入饼图为例子，说明如何在工作表中插入饼图。
### 准备表格

![image](https://user-images.githubusercontent.com/70909689/207043034-62f5276a-718c-4f0e-bec6-eeefddcb8a5f.png)
我们准备在工作表A7单元格处插入宽度为300，高度为260的表格。
### 插入表格要用到的命令

增加一个表格
chartobject.add（left,top,width,height)
设置数据源
chartobhect.chat.setsourcedata()
设置标题
chart.charttitle.text="string"
设置数据标签
chart.ApplyDataLabels (xlDataLabelsShowLabelAndPercent)

### 代码


        Sub insertpie()
          Dim mychartobj As ChartObject
          Dim mychart As Chart
          Dim left, top As Double
          left = Range("A7").left
          top = Range("A7").top
          Set mychartobj = ThisWorkbook.Sheets(1).ChartObjects.Add(left, top, 300, 260)
          Set mychart = mychartobj.Chart
          With mychart
              .ChartType = xlPie
              .SetSourceData Source:=Range("A1:C5")
              .ChartTitle.Text = "市值/成本"
              .ApplyDataLabels (xlDataLabelsShowLabelAndPercent)
          End With
       end sub
#### 运行结果如下图

![image](https://user-images.githubusercontent.com/70909689/207062793-49284b73-1c04-424a-8305-aa41a6022a0b.png)

好，这就是用VBA代码在excel中添加饼图的方法。欢迎联系[ctnhb@126.com](mailto:ctnhb@126.com)



