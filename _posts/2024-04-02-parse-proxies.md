---
layout: post
title: "vless节点解析，让python帮我们搓节点"
date: 2024-04-02
description: "让python帮我们建立节点"
tag: python
---  
我们在上网的时候，经常会用到vless节点，而且我们要经常手动进行设置，如使用优选IP，域名或更换不同的端口，是一项较为繁琐的工作。有的时候会浪费我们大量的时间来进行设置然后才能上网，那么有什么办法能够减轻我们的劳动，提高设置的效率呢？那么，能不能使用python来编一段程序来解决这个问题呢？下面我们做一个探讨，因为我也是一个小白，只能慢慢摸索。  

### 解析vless节点  

要想达到让程序帮我们处理节点的目的，首先我们要对vless节点进行分析，然后再看能否使用python进行编程，我随便拿出一个节点来举个例子；
vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none＃123  

vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:80?security=&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none＃123  

１．“vless://”这代表vless节点的开头；  　　

２．“ebfdccb6-7416-4b6e-860d-98587344d500”是节点的“UUID”；  　

３.“＠”是分隔符；　  　

４．“fbi.gov”是IP地址或是优选域名；　  　

５．“：”是IP和端口的分隔符；  　　

６．“４４３”是端口号；  　　

７.“？”是分割符；  　

８.“security=tls”是传输层安全，表示是否打开ｔｌｓ；　  　

９．后面直到“＃”是伪装域名，传输协议，路径，加密等；  

１０.“＃”是分隔符；  

１１.“１２３”是节点名称。  

### 编程思路  

经过上面的解析，我们已经清楚vless节点的构成了，那么我们怎么把一个几点同过python来编程得到一系列不同端口的节点呢？通过观察我们发现只要我们得到节点的“UUID”、IP或域名并加上节点的名称就可以通过字符串拼接来得到相应的节点。然后我们把得到的节点写入到文件中，这样就能实现把一个节点变为13个节点了，即cloud flare支持的端口，然后对这些节点进行测速就可以选定快速的节点了。
为了方便我么把节点解析程序定义为一个函数，以后方便调用。另外，我把节点名称命名为IP+端口号了，这个可以自行指定，直接上代码：
```


def parse_proxies(str):
    port_tuple_01=('443','2053','2083','2087','2096','8443')
    port_tuple_02=('80','8080','8880','2052','2082','2086','2095')
    str_01=str.lstrip('vless://')           # 去掉vless://
    str_01=str_01.split('#')[0]             # 去掉名称
    print('str_01=',str_01)

    num=str_01.find('?')
    # print(num)
    str_02=str_01[:num]             # uuid@ip:port
    uuid=str_02.split('@')[0]       # uuid
    ip=str_02.split('@')[1].split(':')[0]       # ip
    port=str_02.split('@')[1].split(':')[1]
    print('uuid:',uuid)
    print('ip:',ip)
    print('port:',port)
    str_03=str_01[num+1:]           # security=&sni=anyfast.hhengfa.link&fp=random&type=ws&path=/argox-vl?ed%3D2048&host=anyfast.hhengfa.link&encryption=none
    # print(str_02)
    # print(str_03)
    num=str_03.find('&')
    # print(num)
    str_04=str_03[:num]             # 传输层安全none or tls
    str_05=str_03[num+1:]
    print('security为：',str_04)
    print('其余str_05字符为：',str_05)
    filepath='../解析上网节点/proxie.txt'
    with open(filepath,'w') as f:
        for element in port_tuple_01:
            # print('port:',element,type(element))
            txt='vless://'+uuid+'@'+ip+':'+element+'?'+'security=tls&'+str_05+'#'+ip+':'+element
            print(txt)
            f.write(txt+'\n')
        for element in port_tuple_02:
            txt=txt='vless://'+uuid+'@'+ip+':'+element+'?'+'security=none&'+str_05+'#'+ip+':'+element
            print(txt)
            f.write(txt + '\n')

str='vless://ebfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#123'
parse_proxies(str)


```

通过运行以上代码我们将得到一下节点：

```
vless://bfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi.gov:443
vless://bfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:2053?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi.gov:2053
vless://bfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:2083?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi.gov:2083
vless://bfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:2087?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi.gov:2087
vless://bfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:2096?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi.gov:2096
vless://bfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:8443?security=tls&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi.gov:8443
vless://bfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:80?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi.gov:80
vless://bfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:8080?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi.gov:8080
vless://bfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:8880?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi.gov:8880
vless://bfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:2052?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi.gov:2052
vless://bfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:2082?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi.gov:2082
vless://bfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:2086?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi.gov:2086
vless://bfdccb6-7416-4b6e-860d-98587344d500@fbi.gov:2095?security=none&sni=lg1.freessr2.xyz&fp=chrome&type=ws&path=/xyakws&host=lg1.freessr2.xyz&encryption=none#fbi.gov:2095

```

把以上节点复制粘贴到客户端就可以使用了，省的我们一个一个搓了。如有问题可联系我。




