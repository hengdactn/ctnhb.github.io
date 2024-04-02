---
layout: post
title: "vless节点解析，让python版我们搓节点"
date: 2024-04-02
description: "让python版本我们建立节点"
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

１１.“１２３”是名称。  

### 编程思路  

经过上面的解析，我们已经清楚vless节点的构成了，那么我们怎么把一个几点同过python来编程得到一系列不同端口的节点呢？通过观察我们发现只要我们得到节点的“UUID”、IP或域名并加上节点的名称就可以通过字符串拼接来得到相应的节点。然后我们把得到的节点写入到文件中，这样就能实现把一个节点变为13个节点了，即cloud flare支持的端口，然后对这些节点进行测速就可以选定快速的节点了。




