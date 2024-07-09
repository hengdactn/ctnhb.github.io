---
layout: post
title: "python每隔n分钟运行一次程序"
date: 2024-07-09
description: "python每隔n分钟运行一次程序"
tag: python
---  
在我们编程时，有时需要程序每隔几分钟运行一次，比如，我们每隔5分钟查询一下股票数据。  
于是就编了一小段程序来实现这个功能。

代码如下：
```
import time

def run_subprocess():
    # 运行你的子程序或命令
    print(time.strftime('%Y-%m-%d %H:%M:%S', time.localtime(time.time())),"运行子程序...")
    time.sleep(5)  # 模拟子程序运行时间为5秒
    print("子程序运行完毕！")

def should_run_at_this_time(timer):
    # 获取当前时间的秒数
    current_time = time.localtime()
    current_second = (current_time.tm_min % timer) * 60 + current_time.tm_sec
    # 检查是否在特定时间范围内（4分40秒到5分之间）
    return current_second >= (timer-1) * 60 + 40 and current_second < timer * 60
# 标记变量，用于确保每个特定时间点只运行一次
last_run_time = 0
# 主循环，每秒钟检查一次是否到达特定的运行时间范围
while True:
    if should_run_at_this_time(5):
        # 确保在特定时间范围内只运行一次
        if last_run_time is None or time.time() - last_run_time >= 60:
            run_subprocess()
            # 更新上次运行的时间
            last_run_time = time.time()

    time.sleep(1)  # 每秒钟检查一次


```
把要执行的程序放入到run_subprocess()中即可实现。
