---
layout: post
title: "vless节点解析，让python帮我们搓节点（二）"
date: 2024-04-04
description: "让python帮我们建立节点"
tag: python
---    


上次，通过对vless节点的解析，分析清楚了vless节点的构造，同时也实现了让python帮我们自动化生成节点，省去了我们手动搓节点环节。通过程序，一个节点可以迅速的被构造成为13个节点，那么我们能不能把优选IP或是优选节点也能自动化生成节点呢？经过几天实验，答案是肯定的。我个人感觉优选节点对于我们个人用户来说还是有些繁琐和不稳定，那么优选域名就稳定和简单多了，也减少了节点的数量。  

###  思路  

引入一个优选节点的list（列表），通过增加一个遍历list的循环，把每一个优选域名通过上一篇文章中的方法构造节点，以实现自动化构造优选域名节点。  

### 代码  

不多解释了，还以上次的节点为例，直接代码：
```
import os
# 优选域名
domains=[  'visa.com',
  'visakorea.com',
  'skk.moe',
  'cip.951535.xyz',
  'acjp.cloudflarest.link',
  'acjp2.cloudflarest.link',
  'acsg2.cloudflarest.link',
  'acsg3.cloudflarest.link', ]
# Cloudflare Port
port_tuple_01 = ('443', '2053', '2083', '2087', '2096', '8443')
port_tuple_02 = ('80', '8080', '8880', '2052', '2082', '2086', '2095')

str='vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#123'

vps_name='fbi'                  # 名称注释内容例如VPS名称等

text=str.split('#')[0]             # 去掉节点名称（#及后面内容）
num=text.find('@')
str_0=text[:num+1]

str_1=text[num+1:]
num=str_1.find('?')
ip=str_1[:num].split(':')[0]           # 取得ip

domains.append(ip)                      # 添加自己节点的IP到domains
str_1=str_1[num+1:]
num=str_1.find('&')
str_1=str_1[num+1:]                   # 取得节点剩余字符

filepath = '../解析上网节点/proxie.txt'   # 文件路径
if os.path.exists(filepath):            # 如果存在节点文件则删除
    os.remove(filepath)

with open(filepath, 'a') as f:
    for domain in domains:
        for port in port_tuple_01:
            coment=vps_name+'_'+domain.split('.')[0]+':'+port
            txt = str_0  + domain + ':' + port + '?security=tls&' + str_1 + '#'+coment
            f.write(txt + '\n')
        for port in port_tuple_02:
            coment = vps_name + '_' + domain.split('.')[0]+':'+port
            txt = str_0 + domain + ':' + port + '?security=none&' + str_1 + '#'+coment
            f.write(txt + '\n')




```

生成的节点如下

```
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visa.com:443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visa:443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visa.com:2053?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visa:2053
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visa.com:2083?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visa:2083
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visa.com:2087?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visa:2087
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visa.com:2096?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visa:2096
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visa.com:8443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visa:8443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visa.com:80?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visa:80
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visa.com:8080?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visa:8080
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visa.com:8880?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visa:8880
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visa.com:2052?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visa:2052
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visa.com:2082?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visa:2082
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visa.com:2086?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visa:2086
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visa.com:2095?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visa:2095
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visakorea.com:443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visakorea:443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visakorea.com:2053?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visakorea:2053
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visakorea.com:2083?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visakorea:2083
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visakorea.com:2087?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visakorea:2087
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visakorea.com:2096?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visakorea:2096
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visakorea.com:8443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visakorea:8443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visakorea.com:80?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visakorea:80
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visakorea.com:8080?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visakorea:8080
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visakorea.com:8880?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visakorea:8880
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visakorea.com:2052?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visakorea:2052
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visakorea.com:2082?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visakorea:2082
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visakorea.com:2086?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visakorea:2086
vless://ebfdccb6-7416-4b6e-860d-98587344d500@visakorea.com:2095?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_visakorea:2095
vless://ebfdccb6-7416-4b6e-860d-98587344d500@skk.moe:443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_skk:443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@skk.moe:2053?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_skk:2053
vless://ebfdccb6-7416-4b6e-860d-98587344d500@skk.moe:2083?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_skk:2083
vless://ebfdccb6-7416-4b6e-860d-98587344d500@skk.moe:2087?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_skk:2087
vless://ebfdccb6-7416-4b6e-860d-98587344d500@skk.moe:2096?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_skk:2096
vless://ebfdccb6-7416-4b6e-860d-98587344d500@skk.moe:8443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_skk:8443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@skk.moe:80?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_skk:80
vless://ebfdccb6-7416-4b6e-860d-98587344d500@skk.moe:8080?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_skk:8080
vless://ebfdccb6-7416-4b6e-860d-98587344d500@skk.moe:8880?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_skk:8880
vless://ebfdccb6-7416-4b6e-860d-98587344d500@skk.moe:2052?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_skk:2052
vless://ebfdccb6-7416-4b6e-860d-98587344d500@skk.moe:2082?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_skk:2082
vless://ebfdccb6-7416-4b6e-860d-98587344d500@skk.moe:2086?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_skk:2086
vless://ebfdccb6-7416-4b6e-860d-98587344d500@skk.moe:2095?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_skk:2095
vless://ebfdccb6-7416-4b6e-860d-98587344d500@cip.951535.xyz:443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_cip:443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@cip.951535.xyz:2053?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_cip:2053
vless://ebfdccb6-7416-4b6e-860d-98587344d500@cip.951535.xyz:2083?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_cip:2083
vless://ebfdccb6-7416-4b6e-860d-98587344d500@cip.951535.xyz:2087?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_cip:2087
vless://ebfdccb6-7416-4b6e-860d-98587344d500@cip.951535.xyz:2096?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_cip:2096
vless://ebfdccb6-7416-4b6e-860d-98587344d500@cip.951535.xyz:8443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_cip:8443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@cip.951535.xyz:80?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_cip:80
vless://ebfdccb6-7416-4b6e-860d-98587344d500@cip.951535.xyz:8080?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_cip:8080
vless://ebfdccb6-7416-4b6e-860d-98587344d500@cip.951535.xyz:8880?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_cip:8880
vless://ebfdccb6-7416-4b6e-860d-98587344d500@cip.951535.xyz:2052?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_cip:2052
vless://ebfdccb6-7416-4b6e-860d-98587344d500@cip.951535.xyz:2082?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_cip:2082
vless://ebfdccb6-7416-4b6e-860d-98587344d500@cip.951535.xyz:2086?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_cip:2086
vless://ebfdccb6-7416-4b6e-860d-98587344d500@cip.951535.xyz:2095?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_cip:2095
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp.cloudflarest.link:443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp:443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp.cloudflarest.link:2053?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp:2053
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp.cloudflarest.link:2083?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp:2083
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp.cloudflarest.link:2087?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp:2087
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp.cloudflarest.link:2096?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp:2096
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp.cloudflarest.link:8443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp:8443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp.cloudflarest.link:80?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp:80
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp.cloudflarest.link:8080?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp:8080
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp.cloudflarest.link:8880?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp:8880
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp.cloudflarest.link:2052?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp:2052
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp.cloudflarest.link:2082?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp:2082
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp.cloudflarest.link:2086?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp:2086
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp.cloudflarest.link:2095?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp:2095
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp2.cloudflarest.link:443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp2:443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp2.cloudflarest.link:2053?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp2:2053
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp2.cloudflarest.link:2083?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp2:2083
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp2.cloudflarest.link:2087?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp2:2087
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp2.cloudflarest.link:2096?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp2:2096
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp2.cloudflarest.link:8443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp2:8443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp2.cloudflarest.link:80?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp2:80
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp2.cloudflarest.link:8080?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp2:8080
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp2.cloudflarest.link:8880?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp2:8880
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp2.cloudflarest.link:2052?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp2:2052
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp2.cloudflarest.link:2082?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp2:2082
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp2.cloudflarest.link:2086?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp2:2086
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acjp2.cloudflarest.link:2095?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acjp2:2095
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg2.cloudflarest.link:443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg2:443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg2.cloudflarest.link:2053?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg2:2053
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg2.cloudflarest.link:2083?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg2:2083
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg2.cloudflarest.link:2087?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg2:2087
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg2.cloudflarest.link:2096?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg2:2096
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg2.cloudflarest.link:8443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg2:8443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg2.cloudflarest.link:80?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg2:80
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg2.cloudflarest.link:8080?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg2:8080
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg2.cloudflarest.link:8880?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg2:8880
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg2.cloudflarest.link:2052?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg2:2052
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg2.cloudflarest.link:2082?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg2:2082
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg2.cloudflarest.link:2086?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg2:2086
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg2.cloudflarest.link:2095?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg2:2095
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg3.cloudflarest.link:443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg3:443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg3.cloudflarest.link:2053?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg3:2053
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg3.cloudflarest.link:2083?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg3:2083
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg3.cloudflarest.link:2087?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg3:2087
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg3.cloudflarest.link:2096?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg3:2096
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg3.cloudflarest.link:8443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg3:8443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg3.cloudflarest.link:80?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg3:80
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg3.cloudflarest.link:8080?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg3:8080
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg3.cloudflarest.link:8880?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg3:8880
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg3.cloudflarest.link:2052?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg3:2052
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg3.cloudflarest.link:2082?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg3:2082
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg3.cloudflarest.link:2086?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg3:2086
vless://ebfdccb6-7416-4b6e-860d-98587344d500@acsg3.cloudflarest.link:2095?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_acsg3:2095
vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_fbi:443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:2053?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_fbi:2053
vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:2083?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_fbi:2083
vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:2087?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_fbi:2087
vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:2096?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_fbi:2096
vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:8443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_fbi:8443
vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:80?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_fbi:80
vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:8080?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_fbi:8080
vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:8880?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_fbi:8880
vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:2052?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_fbi:2052
vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:2082?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_fbi:2082
vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:2086?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_fbi:2086
vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:2095?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi_fbi:2095

```

以上程序完成了对一个给定的节点进行自动套用优选域名和端口从而自动化生成节点，如给定一个普通节点，通过程序则可生成117个节点，通过测速可迅速找出快速节点，从而实现节点自由。
通过实验以上代码对Tr节点也是有效的。如有问题，欢迎联系，谢谢！

