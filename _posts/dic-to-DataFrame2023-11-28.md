---
layout: post
title: "python字典转换为Pandas DataFrame"
date: 2023-11-28
description: "dic转Pandas DataFrame"
tag: python
--- 
我们在python实际编程过程中可能会遇到把dic转换为Pandas DataFrame的情况，下面我们探讨一下如何实现。

### 在Pandas DataFrame中将键转换为列，将键值转换为行
	import pandas as pd
	
	dic={'askPx': '78.88',
		 'askSz': '169',
		 'bidPx': '78.87',
		 'bidSz': '269',
		 'high24h': '78.98',
		 'instId': 'TRB-USDT-SWAP',
		 'instType': 'SWAP',
		 'last': '78.87',
		 'lastSz': '123',
		 'low24h': '73.66',
		 'open24h': '78.22',
		 'sodUtc0': '77.89',
		 'sodUtc8': '77.04',
		 'ts': '1701172405707',
		 'vol24h': '12354880',
		 'volCcy24h': '1235488'}
	df=pd.DataFrame([di])
	print(df)
输出:  
		  instType         instId   last lastSz  askPx askSz  bidPx bidSz open24h high24h low24h volCcy24h    vol24h             ts sodUtc0 sodUtc8
	0     SWAP  TRB-USDT-SWAP  78.87    123  78.88   169  78.87   269   78.22   78.98  73.66   1235488  12354880  1701172405707   77.89   77.04

### dic的键转换为行，并添加标题行


		import pandas as pd

		dic={'askPx': '78.88',
			 'askSz': '169',
			 'bidPx': '78.87',
			 'bidSz': '269',
			 'high24h': '78.98',
			 'instId': 'TRB-USDT-SWAP',
			 'instType': 'SWAP',
			 'last': '78.87',
			 'lastSz': '123',
			 'low24h': '73.66',
			 'open24h': '78.22',
			 'sodUtc0': '77.89',
			 'sodUtc8': '77.04',
			 'ts': '1701172405707',
			 'vol24h': '12354880',
			 'volCcy24h': '1235488'}
		df=pd.DataFrame(list(dic.items()),columns=['项目','数值']
		print(df)
输出：  

		           项目             数值
			0       askPx          78.88
			1       askSz            169
			2       bidPx          78.87
			3       bidSz            269
			4     high24h          78.98
			5      instId  TRB-USDT-SWAP
			6    instType           SWAP
			7        last          78.87
			8      lastSz            123
			9      low24h          73.66
			10    open24h          78.22
			11    sodUtc0          77.89
			12    sodUtc8          77.04
			13         ts  1701172405707
			14     vol24h       12354880
			15  volCcy24h        1235488
		