---
layout: post
title: "使用VBA生成随机手机号码"
date: 2032-01-06
description: "随机号码"
tag: VBA
---
在学习和工作中，有时我们会遇到让你填入一个手机号码（不需要验证），我们还得费脑筋想一下，下面我们就用VBA写个小程序，来产生一个随机的手机号码，方便我们使用。VBA的代码如下：
    Public Sub RandPhoneNum()
      '产生随机手机号码
      Dim prenum As String
      Dim rearnum As Long
      prenum = Choose(Application.RandBetween(1, 16), "130", "131", "132", "133", _
          "135", "136", "137", "138", "139", "150", "151", "152", _
          "180", "186", "187", "189")
      rearnum = Application.RandBetween(10000000, 99999999)
      Sheets("随机号码").Cells(1, 3) = prenum & rearnum
  End Sub
这里主要是用到了随机函数函randbetween（）和choose函数。
###1.RANDBETWEEN（）函数
语法：
    RANDBETWEEN（bottom,top）
含义：
  返回位于两个指定数之间的一个随机整数。 每次计算工作表时都将返回一个新的随机整数。
注：在VBA中使用函数前面需要加上Application.
###2.CHOOSE()函数
语法：
    Choose(index_num, value1, [value2], ...)
语法参数：
####1、index_num：必需，用于指定所选定的数值参数。index_num 必须是介于 1 到 254 之间的数字，或是包含 1 到 254 之间的数字的公式或单元格引用。
如果 index_num 为 1，则 CHOOSE 返回 value1；如果为 2，则 CHOOSE 返回 value2，以此类推。
如果 index_num 小于 1 或大于列表中最后一个值的索引号，则 CHOOSE 返回 #VALUE! 错误值。
如果 index_num 为小数，则在使用前将被截尾取整。
####2、value1, value2, ... Value1 是必需的，后续值是可选的。 1 到 254 个数值参数，CHOOSE 将根据 index_num 从中选择一个数值或一项要执行的操作。 参数可以是数字、单元格引用、定义的名称、公式、函数或文本。
