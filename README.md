# Analysing-stocks-by-python


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



data = pd.concat([xu100['Open'],isgyo['Open'],thyao['Open'],eregl['Open'],krdmd['Open'],skbnk['Open']],axis = 1)
data.columns = ['XU100.ISOpen','ISGYO.ISOpen','THYAO.ISOpen','EREGL.ISOpen','KRDMD.ISOpen','SKBNK.ISOpen']
scatter_matrix(data, figsize = (18,8), hist_kwds= {'bins':250})
