---
layout: post
title: "CCXT如何设置代理访问Okx"
date: 2023-11-19
description: "CCXT设置代理访问Okx"
tag: python_okx
--- 
我们使用python通过ccxt访问okx时，可能会有无法访问的情况，那么我们可以通过设置代理的方法实现对okx的访问。

代码如下:
  import ccxt
  ### API初始化
  apikey = '你的apikey'
  secretkey = '你的secretkey'
  passphrase = '你的password'
  ### 实例化交易所并设置代理
  okx = ccxt.okx({
      'proxies': {
          'http': 'http://127.0.0.1:XXXX',
          'https': 'http://127.0.0.1:XXXX'
      }
  })
  
  ### 设置apikey
  okx.apiKey = apikey
  okx.secret = secretkey
  okx.password = passphrase
  
通过以上设置就可以正常访问okx了。  

  


  
