# Time-Series-with-machine-learning

We encounter time-series related tasks everyday, for example: what will happen with our metrics in the next day/week/month/etc., how many user will install our app, how much time will they spend online, how many actions will users complete, and so on. From what I learned and did in work recently, I summarize some main approaches people use in the industry. 

Main approaches:  

- SARIMA (and other basic TS models, like ARIMA, Holt-Winters model, etc.): test stationarity - get rid of non-stationarity – get rid of seasonal difference – build model  

Outdated, time-consuming, require frequent re-training on new data, difficult to tune, only capture information about 'time' 

- ML model 

Linear models: need feature engineering 

Tree-based models: directly, need huge feature engineering; or indirectly, we can forecast trend separately with a linear model and then add predictions from XGB to get a final forecast. 

- FB Prophet  

- LSTMs and RNNs 


Fairly saying, most of machine learning models probably are not very reasonable or make sense with time-series data, since in most cases, we assume our data are independent which obviously doesn't hold with time series. But what if we only care about the accuracy and luckily, with some beautiful transformation and feature engineering we can get a good result with machine learning models? It's 'cheap' and 'good enough', especially considering the time we spend on the SARIMA model and the only 'fair' result from it. We could just try it and see what will happen.
