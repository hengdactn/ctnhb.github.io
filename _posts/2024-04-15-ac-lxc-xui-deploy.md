---
layout: post
title: "AC云IPV6 VPS部署（二）XUI部署"
date: 2024-04-15
description: "AC云IPV6 VPS部署"
tag: 上网
--- 
上一篇我们购买了AC云的VPS，下面我们继续在VPS上安装warp，安装XUI来部署节点。  
### 一、准备工作
#### 1.安装“warp”用到的命令
warp 安装命令：
```
wget -N https://gitlab.com/fscarmen/warp/-/raw/main/menu.sh && bash menu.sh [option] [lisence/url/token]

```
#### 2.安装“XUI”用到的命令  
安装“XUI”用到的命令：  

```
bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
```

#### 3.电脑上要安装warp  

如果你的网络不支持IPV6，需要在电脑上安装warp，安装方法不再细述。  


### 二、登录“anyfastcloud”网站并进入到“My Dashboard”  

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/bfad3518-69f0-4b16-bcd2-c4bebd0a9b68)  

选择我们要部署的服务器，点击“管理”按钮。  

### 三、进入“产品详情”页面  

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/174ae689-3e01-48a5-a6a9-af026dce0769)  

记录好自己的用户名，和IP地址（IPV6）。  


### 四、点击网页的右上方的“网页版ssh”  

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/a467d6e6-f3f3-4254-95a6-f349d4716e32)  

### 五、进入网页版SSH  

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/1cb5bbe1-d453-4ee8-a285-958798fd06f6)  

填写你的IP，端口22不用改，然后填写你的用户名和密码。点击“connect”。  如不能正常登录则运行warp后再次进行登录。

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/3d5a7155-5551-42c9-8d75-67a874c458ef)


### 登录SSH安装warp    

复制我们前面提到的warp命令回车

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/2bde17cc-b884-420d-b0eb-7faa5dbead0c)

### 安装XUI
复制前面提到的XUI命令然后回车  

安装过程中注意修改端口，设置xui的登录信息，用户名和密码。

### 登录XUI

在地址栏输入IPV6地址+端口进入XUI登录页面。输入用户名和密码登录。

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/48cbd779-5ce9-4a43-b692-3f5507ab4831)

### 添加入站    

点击入站列表，选择添加入站  

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/ae31e5b3-7e97-4910-b703-56ae3086133b)  

填写入站信息，端口可以改成80，传输选择ws，path自己定，其它不用改了，然后点添加。

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/1c70ff72-f24f-4772-b21b-75dc0b0066dd)  

点击二维码，等二维码出现后，点击复制。

### 添加节点开始上网

打开我们的上网软件，粘贴我们复制的节点，设置为活动状态，就可以开始上网了。






 









