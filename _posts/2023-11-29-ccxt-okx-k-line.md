---
layout: post
title: "通过CCXT获取okx的K线数据（一）"
date: 2023-11-29
description: "通过CCXT获取okx的K线数据"
tag: python_okx
--- 

想要获取K线数据，目前有两种方法，一种是通过okx的request方法获得，及访问相应的endpoint来获取K线数据；另外一种是通过ccxt来获取。
### 我们先讨论通过request方法获取K线数据
通过阅读okx的API文档，我们发现获取K线获取的是公共数据，所以获取数据不需要APIKEY。直接用request方法就可以。参考文档链接（[获取交易产品K线数据](https://www.okx.com/docs-v5/zh/?python#order-book-trading-market-data-get-candlesticks)）

### 构建一个链接，
根据文档要求我们首先要构造一个连接由baseurl、endpoint和请求参数组成，即：    

    	baseurl='https://www.okx.com'
		endpoint= '/api/v5/market/candles'
		params='?instId=TRB-USDT-SWAP&bar=15m&limit=1440'  
  
这样URL=baseurl+endpoint+params最终的url为：  

https://www.okx.com/api/v5/market/candles?instId=TRB-USDT-SWAP&bar=15m&limit=1440
 
### 通过request方法访问连接并得到返回值
 
		response=requests.get(url,timeout=10)
		print(response.txt）  
  
把K线限制为5条运行结果如下：

		{"code":"0","msg":"","data":[["1701225000000","78.71","78.71","78.31","78.45","39950","3995","313656.303","0"],["1701224100000","78.38","78.73","78.34","78.71","88325","8832.5","693968","1"],["1701223200000","78.22","78.46","77.97","78.39","54019","5401.9","422247.958","1"],["1701222300000","78.47","78.48","78.11","78.22","43470","4347","340133.513","1"],["1701221400000","78.32","78.54","78.24","78.47","74267","7426.7","582342.718","1"]]}
### 通过json把结果格式化
		response=response.json()
		print(response)  
  
运行结果如下：

		{'code': '0', 'msg': '', 'data': [['1701225000000', '78.71', '78.71', '78.31', '78.43', '46159', '4615.9', '362352.682', '0'], ['1701224100000', '78.38', '78.73', '78.34', '78.71', '88325', '8832.5', '693968', '1'], ['1701223200000', '78.22', '78.46', '77.97', '78.39', '54019', '5401.9', '422247.958', '1'], ['1701222300000', '78.47', '78.48', '78.11', '78.22', '43470', '4347', '340133.513', '1'], ['1701221400000', '78.32', '78.54', '78.24', '78.47', '74267', '7426.7', '582342.718', '1']]}

我们提取一下“data	”数据
		
		response=response.json()['data']
		print(response)  
  
运行结果如下：

		[['1701225000000', '78.71', '78.71', '78.31', '78.41', '51101', '5110.1', '401103.898', '0'], ['1701224100000', '78.38', '78.73', '78.34', '78.71', '88325', '8832.5', '693968', '1'], ['1701223200000', '78.22', '78.46', '77.97', '78.39', '54019', '5401.9', '422247.958', '1'], ['1701222300000', '78.47', '78.48', '78.11', '78.22', '43470', '4347', '340133.513', '1'], ['1701221400000', '78.32', '78.54', '78.24', '78.47', '74267', '7426.7', '582342.718', '1']]
这就是我们需要的数据，然后我们存入数据库中

		header=['starttime','open','high','low','close','vol','volCcy','volCcyQuote','confirm']
		df=pd.DataFrame(response,columns=header)
		print（df）  
  
运行结果如下：
		
		       starttime   open   high    low  close    vol  volCcy volCcyQuote confirm
		0  1701225900000  78.42  78.44  78.18  78.23  10798  1079.8   84578.276       0
		1  1701225000000  78.71  78.71  78.31  78.41  51291  5129.1  402593.333       1
		2  1701224100000  78.38  78.73  78.34  78.71  88325  8832.5      693968       1
		3  1701223200000  78.22  78.46  77.97  78.39  54019  5401.9  422247.958       1
		4  1701222300000  78.47  78.48  78.11  78.22  43470    4347  340133.513       1
时间还是不对，转换一下：  

		df['starttime'] = pd.to_datetime(df['starttime'], unit='ms')
		print(df)  
  
结果如下：

		                starttime   open   high  ...  volCcy volCcyQuote confirm
		0 2023-11-29 02:45:55.328  78.42  78.44  ...  1468.8  115043.501       0
		1 2023-11-29 02:30:37.824  78.71  78.71  ...  5129.1  402593.333       1
		2 2023-11-29 02:15:20.320  78.38  78.73  ...  8832.5      693968       1
		3 2023-11-29 02:00:02.816  78.22  78.46  ...  5401.9  422247.958       1
		4 2023-11-29 01:44:45.312  78.47  78.48  ...    4347  340133.513       1  

  
程序完成，我们把程序汇总一下：
		
	import requests
	import pandas as pd
	from pprint import pprint
	symbol='TRB-USDT-SWAP'
	timeframe='15m'
	limit=5
	baseurl='https://www.okx.com'
	endpoint= '/api/v5/market/candles'
	params=f'?instId={symbol}&bar={timeframe}&limit={limit}'
	url=baseurl+endpoint+params
	print(url)
	response=requests.get(url)
	print(response.text)
	response = response.json()['data']
	print(response)
	header = ['starttime', 'open', 'high', 'low', 'close', 'vol', 'volCcy', 'volCcyQuote', 'confirm']
	df = pd.DataFrame(response, columns=header)
	df['starttime'] = pd.to_datetime(df['starttime'], unit='ms')
	print(df)  
 
好了，这就是通过request方法获取K线数据的程序。
