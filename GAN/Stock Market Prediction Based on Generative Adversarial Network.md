# Stock Market Prediction Based on Generative Adversarial Network

## Abstract
近期deep learning運用在財務上面包含了： stock market prediction, portfolio optimization, financial information processing and trade execution strategies.

GAN: 
- D:mlp
    - aims to discriminate the real stock data and generated data
- G:lstm
    - 預測closing price
    - mine the data distributions of stocks from given data in stock market and generate data in the same distributions

We choose the daily data on S&P 500 Index and several stocks in a wide range of trading days and try to predict the* daily closing price*.

## 1.Introduction
許多分析和假設都呈現了股票市場是可以預測的
股票市場上的技術性分析理論是種方法，用來預測價格走向，利用過去市場上的資料
Mean Reversion: that the stock price is temporary and tends to move to the average price over time 股價是暫時性的，而且傾向移動至平均價
further development:
Moving Average Reversion(MAR):average of price is the mean of price in a past window of time, e.g. five days [7].

### contributions
1. A novel Generative Adversarial Network (GAN) architecture with Long-Short Term Memory (LSTM) network as the generator and Multi-Layer Perceptron (MLP) as the discriminator is proposed. The model trained in and end-to-end way to predict the daily closing price by giving the stock data in several past days. 
2. We try to generate the same distributions of the stock daily data through the adversarial learning system, instead of only utilizing traditional regression methods for the price forecasting. 

## 2.Related Work
ARIMA
- perform well in linear and stationary time series
- but not well on the nonlinear and non-stationary data in stock market

combine ARIMA with SVM
- linear part + non-linear part
- linear part: ARIMA
- non-linear part: SVM

combine the wavelet basis with SVM
- decompose the stock data with wavelet transformation
- use SVM for forecasting
- ANN(Artificial Neural Network) combined with ARIMA to predict the nonlinear part of the stock price data
    - effective features should be extracted for the training of ANN

CNN
- used in forecasting stock prices from the limit order book

## 3.Our Methodology

### 3.1 Principle

### 3.2 The Generator
- LSTM
    - time series data
    - daily data in the last 20 years / 7 financial factors
    - predict the future closing price
- 7 factors 1 day (use as 7 features)
    - High Price
    - Low Price
    - Open Price
    - Close Price
    - Volume
    - Turnover Rate
    - Ma5 (the average of closing price in past 5 days)

> The 7 factors are valuable and significant in price prediction with the theory of technical analysis, Mean Reversion, or MAR.
> 

* input: daily stock data of t days
```
X = {x1,x2,......,xt}
```
* each xk in X is a vector composed of 7 features
![](https://i.imgur.com/EkaMDOL.png)

* output of the LSTM: ht
* ht put into fully connected layer with 7 neurons
    * generate ![](https://i.imgur.com/xwcP47X.png)
    * which 估計 ![](https://i.imgur.com/QUjgGTf.png)
    * 取其中的close price 當作t+1那天對closing price的預估值

- LSTM
    - input of the LSTM:
    ![](https://i.imgur.com/TEhYkSk.png)
    - output of the LSTM:
    ![](https://i.imgur.com/ebX16C3.png)

![](https://i.imgur.com/qddBKW7.png)

- ![](https://i.imgur.com/eko8Rvg.png)
    - ![](https://i.imgur.com/ASSc6L2.png) as Leaky ReLU 
    - ![](https://i.imgur.com/ApnT5Tv.png) weight and bias in fully connected layer
    - also using Dropout as regularization method

### 3.3 The Discriminator
function D
- MLP with 3 hidden layers: 
    - h1(72) LeakyReLU
    - h2(100) LeakyReLU
    - h3(10) LeakyReLU
- output layer
    - 0:fake data, 1:real data
    - Sigmoid
- loss: cross entropy loss optimize MLP
- [ ] discriminator activation function
- [ ] CROSS ENTROPY LOSS


Xfake data
X + ![](https://i.imgur.com/0FKM6DK.png)
= ![](https://i.imgur.com/iM0T9Y4.png)

Xreal data
X + ![](https://i.imgur.com/wlLnT18.png)
= ![](https://i.imgur.com/vI3WwgK.png)


![](https://i.imgur.com/Oxy0Uc3.png)

### 3.4 The Architecture of GAN
![](https://i.imgur.com/HTBiri9.png)
![](https://i.imgur.com/4mUpUl6.png)

> The reason why we put Xfake and Xreal rather than ˆ xt+1 and xt+1 in the discriminator is that we expect the discriminator to capture the correlation and time series information between xt+1 and X. 
> 

## 4. Experiments
### 4.1. Dataset Descriptions
real stock data from Yahoo Finance
- Standard & Poor’s 500 (S&P 500 Index)
- Shanghai Composite Index in China
- International Business Machine (IBM) from New York Stock Exchange (NYSE)
- Microsoft Corporation (MSFT) from National Association of Securities Dealers Automated Quotation (NASDAQ)
- Ping An Insurance Company of China (PAICC)

date: last 20 years
- almost 5000 pieces of data in each stock
- The trade date is not continuous due to the limitation of trading on weekends and holidays

normalization
- MAR 
- ![](https://i.imgur.com/GvcVw3d.png)
    - ![](https://i.imgur.com/TjxjTmI.png)
![](https://i.imgur.com/EvmaPtR.png)
![](https://i.imgur.com/CXrUt0A.png)

t=5
- predict the data using the past one week
> trade is limited on weekends
- For instance, we compute the mean and standard deviation of the data **of 5 days** to normalize the data
Afterwards, the normalized data are used to predict the data on 6th day.
The data in both training and testing periods are processed in the same way.

### 4.2. Training of our model
利用前t天的資料，預測第六天的7 factors並取closing price
> The reason why predicting 7 factors in the next day is that the generator aims to mining the distributions of the real data and we can get the closing price from the generated data
> 90%-95% of the stock data for training and the remaining 5%-10% (about 250-500 pieces of data) for testing. 

There is a significant adversarial process between the discriminator and generator during training. Both the discriminator and generator have been optimized during the adversarial process
![](https://i.imgur.com/PQMfO7Y.png)


### 4.3. Experimental results

evaluate model by
Mean Absolute Error (MAE), Root Mean Square Error (RMSE), Mean Absolute Percentage Error (MAPE) and Average Return (AR)

![](https://i.imgur.com/M7MYUjn.png)


compare with baselines:
Support Vector Regression (SVR), ANN and LSTM are classical methods for stock market prediction

> Low MAE, RMSE and MAPE indicate that the prediction of closing price is approximate to the real data. AR shows the daily average return of these stocks based on four prediction methods.
 
![](https://i.imgur.com/DdXR62q.png)


## 5. Conclusion

![](https://i.imgur.com/Xxh22Ft.png)


