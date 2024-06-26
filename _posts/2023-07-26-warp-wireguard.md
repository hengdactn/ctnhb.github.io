---
layout: post
title: "Win7旧电脑无法安装warp，使用wireguard实现上网"
date: 2023-07-26
description: "将CloudFlare warp的配置导入到wireguard中实现上网"
tag: 上网
---
笔记本电脑是win10，顺利安装warp并实现上网。台式机有点老了，装的还是Win7，想安装warp实现上网，但warp却不支持Win7，没有办法钱前一段时间有一些up提出可以把warp的配置导入到wireguard中，从而实现上个网。为了让老电脑能上网于是就把warp的参数导入到wireguard中，完美实现上网。具体步骤如下：
### 一、需要网站地址
1.wireguard官方网站 

[https://www.wireguard.com/install/](https://www.wireguard.com/install/)

2.生成warp配置的网站（感谢勇哥和不一样的强哥的网站）

[https://replit.com/@kelekekou8/WARPconfig-youtubeBu-Yi-Yang-De-Qiang-Ge](https://replit.com/@kelekekou8/WARPconfig-youtubeBu-Yi-Yang-De-Qiang-Ge)

### 二、下载并安装wireguard
打开wireguard的官方网站，
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/6afb1ae1-db98-49fb-8d09-0b384d527a39)
根据自己的系统选择下载。我这是Win7选择Windows版下载。然后安装。
### 三、打开勇哥的warp配置生成网站
1.打开网站，并点击绿色的“Run”按钮。
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/b142e211-f952-4e02-985e-67b414f9164f)
2.输入2并回车
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/56035c13-1a6a-4349-bffb-205ba53a9b6c)
3.根据你的账户情况输入相应的数字
如果是普通账户就输入1

如果是plus+账号输入2

如果是team账号输入3
我的账号已经升级到team了，则输入3。

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/6b585883-ccb8-46ab-b165-4ddb64f45880)
![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/7789ba38-4761-4bd4-8938-d2ae803cf5e4)

点击图中所示网址

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/48d3750f-71c2-490c-bf4c-3dcbb526bd10)

会打开新的网页要求输入team的名称，我们输入名称并点击go

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/efb19f6e-d6d2-4aa6-81a4-4535327e1391)

然后会让你输入你的邮箱，我们输入邮箱

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/f7846c4e-0b5e-43e7-ac9c-6e52c7fc15f2)

然后会有验证码通过邮件发送给你，我们复制验证码输入到新窗口然后点击登录

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/82a393da-7c81-4d2b-9a9a-4c6f81a3ba68)

然后会打开一个新的窗口显示你的token

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/d2debe19-bcd1-4951-88eb-d872f1e147bc)

复制你的token，粘贴到强哥的网站回车

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/1aeb11ce-2d43-491b-9a67-2015a4fcfd16)

然后回生成wireguard配置

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/671cf054-94c3-454f-ab72-942b750d2fc9)

### 四、打开wireguard

1.打开wireguard

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/edb63c95-9f40-45d7-9019-d6abcff2c6c2)

2.选择新建隧道，新建空隧道

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/a4826559-fa31-4b32-9ebf-f7b275d11364)

3.填写名称并把刚才的配置粘贴到新建隧道中，然后保存

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/dc60f15c-ed03-461a-a118-02c052caa0ee)

### 五、点击刚建立的隧道，并点击连接

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/5e06a3ca-1ade-4479-840d-e735d9b5e4b0)

点击刚建立的隧道，并点击连接，然后就可以上网了。











