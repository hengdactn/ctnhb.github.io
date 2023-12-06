---
layout: post
title: "通过CloudFlare部署订阅链接"
date: 2023-12-06
description: "通过CloudFlare部署订阅链接"
tag: 上网
--- 

当我们上网的时候经常会遇到需要不断更新节点的情况，于是我们四处搜寻节点，而且从网上搜索到的节点有的有效期很短，大大降低了我们的上网的效率，下面我们介绍一种通过CloudFlare来部署节点的订阅链接的方法。
### 需要的资料
1.CloudFlare的注册用户；  
如果不是注册用户可通过下面的链接来注册：  
Cloudflare网站地址：[https://www.cloudflare.com/zh-cn/](https://www.cloudflare.com/zh-cn/)  
2.部署订阅用到的代码； 
代码地址：[workers_sub](https://raw.githubusercontent.com/hengdactn/cf_worker_sub/main/workers_sub.txt)  
### 部署方法  
1.登陆网站后找到左侧侧边栏的Workers&Pages并点击进入；  
2.选择"Create application";  
3.选择"Create Worker";  
4.在"Name"标签下输入订阅的名称;   
5.选择“Editcode”  
6.清楚代码内容，并粘贴以上提供的代码。并选择“Save and deploy”，复制生成链接；  
7.添加域名。          
部署完毕。    
### 使用方法
把添加的域名加“/sub”添加到上网软件的订阅链接里，更新订阅就可以使用了。  
  



