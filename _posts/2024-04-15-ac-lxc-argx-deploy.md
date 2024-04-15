---
layout: post
title: "AC云IPV6 VPS部署（三）隧道部署"
date: 2024-04-15
description: "AC云IPV6 VPS部署"
tag: 上网
---  

上两篇，通过部署xui面板的方法实现了上网，这次我们讨论再通过部署argx隧道来实现上网的方法。

### 一、用到的命令  

```
bash <(wget -qO- https://raw.githubusercontent.com/fscarmen/argox/main/argox.sh)
```

### 二、按照上一章的方法按照warp。  

### 三、 登录网页版SSH  

登录网页版SSH输入上面的命令，根据命令行提示完成安装。
安装完成后会有订阅链接显示出来，把这些链接复制并保持备用。  

### 四、使用节点开始上网  

把上面复制的节点信息粘贴到上网软件中，即可开始上网，粘贴的节点中，只有vmess或一个vless能用，其它的是不能用的。












