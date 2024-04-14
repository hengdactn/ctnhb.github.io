---
layout: post
title: "AC云IPV6 VPS部署（二）通过XUI部署VPS"
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

![image](https://github.com/hengdactn/ctnhb.github.io/assets/70909689/34d204c8-54eb-404a-8c97-a2db4cc3f2f8)








