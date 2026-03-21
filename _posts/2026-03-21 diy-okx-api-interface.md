---
layout: post
title: "自己建立okx的api接口"
date: 2026-03-21
description: "自己建立okx的api接口"
tag: python
---  

我们用python程序进行代币交易时，经常会用到ccxt等的库进行交易。但是，我经常遇到，因为库不完善一些功能现有的库无法实现，再有就是随着库的升级你编写的程序可能不能正常运行，我经常遇到这样的情况。于是，我想能不能自己建立最基础的api接口，然后再通过api接口来实现我们的特定要求。那我们来试一下吧。
通过学习okx的api文档，我们要如下操作：

### 创建自己的APIKey

打开这个链接：https://www.okx.com/zh-hans/account/my-api

如下图：
<img width="1704" height="843" alt="Ashampoo_Snap_2026 03 21_18h34m59s_012_Chrome Legacy Window" src="https://github.com/user-attachments/assets/5cfb1c75-315f-4dd0-a0d2-bc2315603ee5" />



创建APIKey后，您将获得3个必须记住的信息：

* APIKey

* SecretKey

* Passphrase

APIKey和SecretKey将由平台随机生成和提供，Passphrase将由您提供以确保API访问的安全性。平台将存储Passphrase加密后的哈希值进行验证，但如果您忘记Passphrase，则无法恢复，请您通过交易网站重新生成新的APIKey。
#### 注意APIKey 权限
APIKey 有如下3种权限，一个 APIKey 可以有一个或多个权限。

* 读取 ：查询账单和历史记录等 读权限
  
* 提现 ：可以进行提币
  
* 交易 ：可以下单和撤单，转账，调整配置 等写权限
  
为了我们资金的安全一定不要选择”提现“！！！

#### APIKey 安全性
* 每个APIKey最多可绑定20个IP地址，IP地址支持IPv4/IPv6和网段的格式。
 未绑定IP且拥有交易或提币权限的APIKey，将在闲置14天之后自动删除。(模拟盘的 API key 不会被删除)

* 用户调用了需要 APIKey 鉴权的接口，才会被视为 APIKey 被使用。
  
* 调用了不需要 APIKey 鉴权的接口，即使传入了 APIKey的信息，也不会被视为使用过。
  
* Websocket 只有在登陆的时候，才会被视为 APIKey 被使用过。在登陆后的连接中做任何操作（如 订阅/下单），也不会被认为 APIKey 被使用，这点需要注意。
  
用户可以在 安全中心 中看到未绑定IP且拥有交易/提现权限的 APIKey 最近使用记录。

### REST 请求验证

#### 发起请求

所有REST私有请求头都必须包含以下内容：

* OK-ACCESS-KEY字符串类型的APIKey。

* OK-ACCESS-SIGN使用HMAC SHA256哈希函数获得哈希值，再使用Base-64编码（请参阅签名）。

* OK-ACCESS-TIMESTAMP发起请求的时间（UTC），如：2020-12-08T09:08:57.715Z

* OK-ACCESS-PASSPHRASE您在创建API密钥时指定的Passphrase。

所有请求都应该含有application/json类型内容，并且是有效的JSON。

#### 签名

OK-ACCESS-SIGN的请求头是对timestamp + method + requestPath + body字符串（+表示字符串连接），以及SecretKey，使用HMAC SHA256方法加密，通过Base-64编码输出而得到的。

如：sign=CryptoJS.enc.Base64.stringify(CryptoJS.HmacSHA256(timestamp + 'GET' + '/api/v5/account/balance?ccy=BTC', SecretKey))

其中，timestamp的值与OK-ACCESS-TIMESTAMP请求头相同，为ISO格式，如2020-12-08T09:08:57.715Z。

method是请求方法，字母全部大写：GET/POST。

requestPath是请求接口路径。如：/api/v5/account/balance

body是指请求主体的字符串，如果请求没有主体（通常为GET请求）则body可省略。如：{"instId":"BTC-USDT","lever":"5","mgnMode":"isolated"}

 GET请求参数是算作requestPath，不算body
SecretKey为用户申请APIKey时所生成。如：22582BD0CFF14C41EDBF1AB98506286D

### 程序

#### 获取apikey等相关参数

OKX_API_KEY=                            # 你的API_KEY
OKX_SECRET_KEY=                         # 你的Secret_KEY
OKX_PASSPHRASE=                         # 你的Passphrase 

#### 获取时间戳

我们可以定义一个函数来获取时间戳：

  import time
  
  def get_timestamp():
      return time.strftime('%Y-%m-%dT%H:%M:%S.000Z', time.gmtime())

#### 构造签名函数

  def sign(timestamp, method, path, body=""):
  
      message = timestamp + method + path + body
  
      mac = hmac.new(
          SECRET_KEY.encode(),
          message.encode(),
          hashlib.sha256
      )
  
      return base64.b64encode(mac.digest()).decode()





### ANSI 颜色代码主要包括以下几类: 
#### 文本颜色:  
30-37 和90-97 分别代表普通和亮色的文本颜色。例如，31 是红色，91 是亮红色。

| 字体颜色 |背景颜色|颜色描述|
|:----:|:----:|:----:|
| 30 |40|黑色|
| 31 |41|红色|
| 32 |42|绿色|
| 33 |43|黄色|
| 34 |44|蓝色|
| 35 |45|紫红色|
| 36 |46|青色|
| 37 |47|白色|

#### 背景颜色:  
40-47 和100-107 分别代表普通和亮色的背景颜色。例如，42 是绿色背景，102 是亮绿色背景。  
#### 其他属性:  
如加粗(1), 下划线(4), 反色(7) 等。使用0 可以重置所有属性到默认值。  

| 显示方式 |效  果|
|:----:|:----:|
| 0|终端默认设置|
| 1|高亮显示|
| 4|使用下划线|
| 5|闪烁|
| 7|反色显示|
| 8|不可见|


### 示例:
\033[32m 设置文本颜色为绿色(32)。  
\033[45m 设置背景颜色为品红(45)。  
\033[1;31m 设置文本为加粗红色(1, 31)。  
\033[0m 重置所有属性为默认值。﻿  
在终端中使用ANSI 颜色代码:  
在Linux 或macOS 的终端中，可以直接在命令行中使用 echo -e 命令输出带有ANSI 颜色代码的字符串，例如：  
代码  

  echo -e "\033[31mThis is red text\033[0m"  
### 注意事项: 
不是所有终端都完全支持ANSI 转义序列，一些老的终端可能无法正确显示颜色。  ﻿
在Windows 系统上，需要使用支持ANSI 终端的工具，如 Cygwin 或 MinGW，或者使用一些特殊的库来支持ANSI 颜色，博客园 提供了一些方法。﻿  
ANSI 颜色代码可以用于Shell 脚本，使输出更加美观和易于阅读。﻿  
