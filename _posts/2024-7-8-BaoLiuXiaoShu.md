---
layout: post
title: "python保留2位小数的几种方法"
date: 2024-07-08
description: "保留2位小数"
tag: python
---  
python保留2位小数的几种方法汇总。

### 一、‘%.2f’%f

代码如下：
```
num=3.1545926

print('%.2f'%num)
print('%.3f'%num)
print('%.5f'%num)

```
结果如下：

```
3.15
3.155
3.15459
```
可见，该方法会进行四舍五入。

### 二、format函数  

代码如下：
```
num=3.1545926

print('{:.2f}'.format(num))
print('{:.3f}'.format(num))
print('{:.5f}'.format(num))
```
运行结果如下：

```
3.15
3.155
3.15459
```
可见，该方法也会进行四舍五入。

### 三、round（函数）
代码如下：
```
num=3.1545926

print(round(num,2))
print(round(num,3))
print(round(num,4))
print(round(num,5))
```
运行结果如下：
```
3.15
3.155
3.1546
3.15459
```
可见，该方法也会进行四舍五入。

### 四、直接保留2小数，后面去掉  

代码如下
```
num=3.1545926

num=int(num*100)/100
print(num)
```
运行结果如下：

```
3.15
```

以上是几种保留2位小数的方法，欢迎互动。



