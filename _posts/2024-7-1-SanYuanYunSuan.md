---
layout: post
title: "三元运算符让python代码更简洁"
date: 2024-07-01
description: "三元运算符"
tag: python
---  

我们在编程时，经常会用到IF  else语句，列如求较大值：

```
a=30
b=20

if a>b:
    x=a
else:
    x=b

```

这样写给人的感觉既不简介也不优雅，那怎样使代码优雅简洁呢，答案是采用三元运算符。

### 三元运算符
那什么是三元运算符呢？三元运算符是一种由三个操作数组成的运算符，通常用于在条件为真和为假之间进行选择。它具有简洁性：使用三元运算符可以在一个语句中完成相同的操作，而不需要编写额外的if-else代码块或switch-case语句。这使得代码更加简洁易读。
它还具有方便性：通过使用三元运算符，可以更方便地处理只有两种可能结果的操作，比如在赋值操作中使用。速度：相对于if-else语句，三元运算符可以提高代码执行的速度，因为在if-else语句中可能存在多次判断。而由于三元运算符只会执行一次条件判断，所以它可以带来更快的代码执行速度。

### 三元运算写法一 

 变量名=（条件表达式）and 表达式1 or 表达式2 
 
当条件表达式为真时，变量值为表达式1，假时为表达式2。

```
x= a>b and a or b
```
### 三元运算符写法二

变量名=[表达式1,表达式2][条件表达式]

当条件表达式为真时，变量的值为表达式2，条件表达式为假时变量值为表达式1。

```
x=[b,a][a>b]
```

### 三元运算符写法三

变量名=表达式1，IF（条件表达式）else 表达式2  

当条件表达式为真时，变量值为表达式1，假时为表达式2  

```
x=a if a>b else b
```

### 三元运算符写法四

对于真假的判断，可采用这种简单的写法

变量名= 表达式1 and 表达式2

表达式1为加时变量值为假，表达式1为真时变量值为表达式2

False and True  值为False
False and False 值为False
True and True   值为True
True and False  值为False
```
x=a and b 
print(x) # x=20
```

### 三元运算符写法五

同上，用于真假的判断，可采用这种简单的写法  

变量名= 表达式1 or 表达式2

表达式1值为真时，变量值为表达式1
表达式1值为假时，变量值为表达式2

False or True  值为True
False or False 值为False
True or True   值为True
True or False  值为True

```
x=a or b 
print(x)  # x=a
```
### 三元运算符的写法六（嵌套）

```
x= a if a>b else c if c>d else d
```
应理解为：

```
x=a if a>b else (c if c>d esle d)
```

以上就是三元运算符的写法，如有问题欢迎联系我。









