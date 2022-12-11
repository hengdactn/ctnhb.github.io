---
layout: post
title: "Excel VBA 的换行和回车"
date: 2022-12-11
description: "Excel VBA linefeed enter"
tag: VBA
---
在excel VBA使用过程中，我们当一行内容过多或需要分行显示的时，我们就要对内容进行换行。正常换行是换到下一行，但光标的水平位置没有变化，而回车是光标移动到当前行的行首，那么在VBA中换行和回车是什么情况呢。下面我们通过一个程序来验证一下。

  首先我们先了解一下换行和回车的标书方法
  
         chr(10) 可以生成换行符
         chr(13) 可以生成回车符
         vbcrlf 换行符和回车符
         vbCr 等同于chr(10)
         vblf 等同于chr(13)
         
 程序代码
 
         Sub test3()
             MsgBox "~~~~~只换行" & vbCrLf & "换行测试" & Chr(10) & "Excel"
             MsgBox "~~~~~只回车" & vbCrLf & "回车测试" & Chr(13) & "Excel"
             MsgBox "~~~~~换行回车" & vbCrLf & "换行回车测试" & vbCrLf & "Excel"
             MsgBox "~~~~~回车换行" & vbCrLf & "回车换行测试" & Chr(13) & Chr(10) & "Excel"
         End Sub
       
 运行情况如下
 
 ![image](https://user-images.githubusercontent.com/70909689/206899596-88fefbbc-eda5-4128-97d9-aee69a9b9d3b.png)
 ![image](https://user-images.githubusercontent.com/70909689/206899619-764f698a-6bd0-4145-9591-3322c890ede3.png)
 ![image](https://user-images.githubusercontent.com/70909689/206899650-7fc6c0ae-4135-4845-b072-b6cc07c46645.png)
 ![image](https://user-images.githubusercontent.com/70909689/206899704-32de0171-7215-4936-bd71-ec8e8f8cfea7.png)

通过运行结果分析，我们可以发现这几种方法得到的结果是一致的。欢迎联系[ctnhb@126.com](mailto:ctnhb@126.com)
