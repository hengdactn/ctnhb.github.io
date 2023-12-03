---
layout: post
title: "通过CCXT获取okx代币的K线数据（二）"
date: 2023-12-3
description: "获取okx的K线数据"
tag: python_okx
--- 

我们request的方法获取了K线数据，下面我们继续采用引用ccxt库来获取代币的K线数据。
### ccxt简介
1.ccxt简介  
CCXT是一个开源的数字货币交易框架，它封装了全世界绝大多数的交易所API。   
2.安装ccxt  
安装ccxt只需要在命令行中执行：pip install ccxt   
如果安装很慢可以使用国内镜像安装源来安装：   
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple ccxt  
3.引用ccxt  
import ccxt  
### 程序思路
通过ccxt的fetch ohlc函数来获取K线数据具体程序如下：  

		import ccxt
		import pandas as pd
		from datetime import timedelta
		okx=ccxt.okx.()
		symbol='TRB-USDT-SWAP'
		time_frame='15m'
		pd.set_option('display.max_rows',None) # 显示全部行
		data=okx.fetch_ohlcv(symbol=symbol,timeframe=time_frame,limit=1000,params={'paginate':True})
		header=['open_ts','open','high','low','close','vol']
		df=pd.DataFrame(data,columns=header,dtype=float)
		df['open_ts']=pd.to_datetime(df['open_ts'],unit='ms')
		df['open_ts']=df['open_ts']+timedelta(hours=8)
		print(df)    

注：params参数是为了让K线数据不收到300的限制。    

运行结果如下：  
			        open_ts   open   high    low  close       vol  
		0   2023-11-23 10:00:00  98.72  99.85  93.61  94.35  260256.2  
		1   2023-11-23 10:15:00  94.30  95.65  93.80  94.38   84081.3  
		2   2023-11-23 10:30:00  94.38  94.70  94.05  94.40   24458.2  
		3   2023-11-23 10:45:00  94.41  94.66  92.63  92.95   46703.0  
		4   2023-11-23 11:00:00  92.94  93.59  92.40  92.88   48595.9  
		5   2023-11-23 11:15:00  92.90  93.42  92.65  93.36   22065.1  
		6   2023-11-23 11:30:00  93.34  93.54  93.00  93.02   12476.0  
		7   2023-11-23 11:45:00  93.02  93.13  92.22  92.46   20573.0  

数据很多只列出几条做演示。
