# Analysing-stocks-with-python


import pandas as pd

import datetime

import numpy as np

import matplotlib.pyplot as plt

from pandas.plotting import scatter_matrix

!pip install yfinance

import yfinance as yf

%matplotlib inline

start = "2022-01-01"
end = '2022-10-27'
xu100 = yf.download('XU100.IS',start,end)
isgyo = yf.download('ISGYO.IS',start,end)
thyao = yf.download('THYAO.IS',start,end)
eregl = yf.download('EREGL.IS',start,end)
krdmd = yf.download('KRDMD.IS',start,end)
skbnk = yf.download('SKBNK.IS',start,end)



xu100['Volume'].plot(label = 'XU100.IS', figsize = (15,7))
isgyo['Volume'].plot(label = "ISGYO.IS")
thyao['Volume'].plot(label = 'THYAO.IS')
eregl['Volume'].plot(label = 'EREGL.IS')
krdmd['Volume'].plot(label = "KRDMD.IS")
skbnk['Volume'].plot(label = 'SKBNK.IS')
plt.title('Volume of Stock traded')
plt.legend()
 
 ![image](https://user-images.githubusercontent.com/115734646/198324184-0f0217fb-a3cb-4e7c-975c-b1e79590d7dc.png)

 
#Market Capitalisation
xu100['MarktCap'] = xu100['Open'] * xu100['Volume']
isgyo['MarktCap'] = isgyo['Open'] * isgyo['Volume']
thyao['MarktCap'] = thyao['Open'] * thyao['Volume']
xu100['MarktCap'].plot(label = 'XU100.IS', figsize = (15,7))
isgyo['MarktCap'].plot(label = 'ISGYO.IS')
thyao['MarktCap'].plot(label = 'THYAO.İS')
eregl['MarktCap'] = eregl['Open'] * eregl['Volume']
krdmd['MarktCap'] = krdmd['Open'] * krdmd['Volume']
skbnk['MarktCap'] = skbnk['Open'] * skbnk['Volume']
eregl['MarktCap'].plot(label = 'EREGL.IS', figsize = (15,7))
krdmd['MarktCap'].plot(label = 'KRDMD.IS')
skbnk['MarktCap'].plot(label = 'SKBNK.İS')
plt.title('Market Cap')
plt.legend()
 
 ![image](https://user-images.githubusercontent.com/115734646/198324294-03a59b18-8ae4-4795-9a69-bf024affe491.png)


data = pd.concat([xu100['Open'],isgyo['Open'],thyao['Open'],eregl['Open'],krdmd['Open'],skbnk['Open']],axis = 1)
data.columns = ['XU100.ISOpen','ISGYO.ISOpen','THYAO.ISOpen','EREGL.ISOpen','KRDMD.ISOpen','SKBNK.ISOpen']
scatter_matrix(data, figsize = (18,8), hist_kwds= {'bins':250})

![image](https://user-images.githubusercontent.com/115734646/198324364-11352451-6498-4f69-8eb2-4768481ab573.png)


#Volatility
xu100['returns'] = (xu100['Close']/xu100['Close'].shift(1)) -1
isgyo['returns'] = (isgyo['Close']/isgyo['Close'].shift(1))-1
thyao['returns'] = (thyao['Close']/thyao['Close'].shift(1)) - 1
xu100['returns'].hist(bins = 100, label = 'XU100.İS', alpha = 0.5, figsize = (15,7))
isgyo['returns'].hist(bins = 100, label = 'ISGYO.İS', alpha = 0.5)
thyao['returns'].hist(bins = 100, label = 'THYAO.İS', alpha = 0.5)
eregl['returns'] = (eregl['Close']/eregl['Close'].shift(1)) -1
krdmd['returns'] = (krdmd['Close']/krdmd['Close'].shift(1))-1
skbnk['returns'] = (skbnk['Close']/skbnk['Close'].shift(1)) - 1
eregl['returns'].hist(bins = 100, label = 'EREGL.İS', alpha = 0.5, figsize = (15,7))
krdmd['returns'].hist(bins = 100, label = 'KRDMD.İS', alpha = 0.5)
skbnk['returns'].hist(bins = 100, label = 'SKBNK.İS', alpha = 0.5)
plt.legend()

![image](https://user-images.githubusercontent.com/115734646/198324457-5c0ffa34-2a1e-4b35-8cfb-d18655532b30.png)
