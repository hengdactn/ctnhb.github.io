---
layout: post
title: "Cloudflare内搭建机场节点"
date: 2023-07-06
description: "部署CloudFlare workers实现把CloudFlare变为机场功能"
tag: 上网
---
### 简介
通过在CloudFlare的workers部署代码，来实现机场功能。
### 1.登录CloudFlare网站
### 2.选择Workers and Pages
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/296e6ba6-f9e6-4aa0-aaf8-2a91b18cb4a7)
### 3.选择“创建应用程序”
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/27373f70-4185-4807-9d92-425822669569)
### 4.选择“创建worker”
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/296dd201-51fd-4c8e-9277-f4ed65a10a41)
### 5.填写应用程序名称，然后点击“确定”
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/4532ded2-21e2-45fc-8229-f94ac0c85c1b)
### 6.选择“编辑代码”
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/948c0826-7aa4-47c5-9115-e5970ccce09a)
### 7.删除所有代码
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/826dd439-352a-4fe6-867a-1031dff1b3b5)
### 8。复制下方链接中的代码,粘贴到代码框当中，然后点击“保存并部署”
代码链接：https://github.com/hengdactn/ctnhb.github.io/blob/master/workers%E4%BB%A3%E7%A0%81.txt
或：https://raw.githubusercontent.com/leilei223/works/main/index.js
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/d9efcfbf-8a7a-4a92-8581-90e072ddca2c)
### 10.复制此地址
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/0772aeab-5184-43bd-b8a1-659e656587ef)
### 11.打开V2ray，选择“设置”添加新的分组，我们命名为test。
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/2f7b5aac-f10a-483e-b2a9-307a40c5eb7a)
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/b204887d-628e-48d1-9bd1-2b3c09eca3a5)
### 12.选择订阅菜单，选择订阅设置，添加刚才复制的地址，然后再地址后加上sub/和ip地址
ip地址可以用ip优选工具选出或用一下网站选出
网址：https://vfarid.github.io/cf-ip-scanner/?max=30#
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/5f9ea162-806c-4c4e-b6bf-e144b35ccafd)

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/b0a1085c-cde9-40be-8c82-20e35ef8698e)
### 13.更新订阅，如不行就多更新几次。
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/30eb971c-960c-4fdd-86f7-737cd51ea934)
最后对所有的节点进行测速，删除不能用的节点。所有的工作都完成了，可以畅游网络了。





