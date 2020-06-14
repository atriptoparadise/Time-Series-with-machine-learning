# Time-Series-with-machine-learning

See the post at **[Medium](https://medium.com/@qs2178/time-series-forecasting-with-stacked-machine-learning-models-7250abdece0f)**.



---
Welcome! 

I recently finished a project about time series forecasting and I figured it’s time to summarize my work for myself and sharing my thoughts with anyone needs it. As a brief introduction, I am a data scientist at a company selling products for animals.
Let’s start with some questions that I spent some time to figure out and I think it’s also important to know before you go deeper into it.

1. Why need it?

Ya, of course it should be the first question we ask ourselves. So in this project, my objective is to predict future sales as we want to set up the quota for each account, territory (area) and product in the next half year. There’re also tons of other cases, for example, what will happen with our metrics in the next day/week/month/etc., how many users will install our app in the future, how much time will they spend online, how many actions will users complete, what’s stock price in next month, and so on. Basically, they’re all the same, we want to have some basic ideas that what will happen in the future then we can set up some marketing campaigns or strategies, etc.

2. Why machine learning models?

Fairly saying, without any data preprocessing, most machine learning models do not make statistical sense with time-series data since we assume our data are independent which obviously doesn’t hold in time series.

But what if we only care about the accuracy and luckily, after some transformation and feature engineering, we can get a good result by machine learning models? It’s “cheap” and “good” enough, especially considering the time we spend on those traditional models (ARIMA, SARIMA, Holt-Winters model, etc.) and the only “fair” result from it.

Facebook also released a library named “Prophet” in 2017, but the problem of Prophet is also the same with those traditional models, they only capture the “time” (trend & seasonality) information from historical data, what if there’re lot’s of latent patterns behind those apparent trends that people can easily notice by data and domain knowledge? They fail.

We also can use deep learning to deal with time series, but I won’t go through here, if you’re interested in you can see this post.

3. Which models? Why Stacking?

I used Linear regression first then tried adding L1 and L2 regularization into it. Then I did it by XGB and LightGBM which performed better than linear models in test data-set.

For decreasing the variance and better prediction performance, I decided to stack them together to have a final model. The weights of each model were determined by the performance in test data-set.

4. What’s the metric?

Mean Absolute Percentage Error: is a measure of prediction accuracy of a forecasting method in statistics. It expresses accuracy as a percentage, and is similar with MAE but is computed as a percentage, which is very convenient when you want to explain the quality of the model to management, [0,+∞)

![Image description](https://miro.medium.com/max/186/1*Ijk7yK-4f1qfnOQGdVV8iQ.png)

5. How to do the cross-validation?

As time-series has a different structure compared with normal machine learning data-set, we can’t directly randomize all data into train/test set as we did before, since with randomization, all time dependencies between observations will be lost.

I used a more tricky approach in optimizing the model parameters which can be found here. The idea is rather simple — we start with a small subset of data for training purpose, forecast for the later data points and then checking the accuracy for the forecasted data points. The same forecasted data points are then included as part of the next training dataset and subsequent data points are forecasted. The process will be like this:

![Image description](https://miro.medium.com/max/631/1*6ujHlGolRTGvspeUDRe1EA.png)

6. What’s the original data table? What’s the final input in your model? How to do the feature engineering?
Okay, I will just walk through the whole process for this project from this question.

- In summary,

1. Getting data from database
2. EDA & Data Preprocessing based on business need
3. Feature engineering, created 48 months lag features and others
4. Modeling for each model after split; hyper-parameter tuning for tree-based models
5. Measure models performance by MAPE and stacked them into a new model
6. Using all data with the stacked model to do the final prediction

- Note: Due to confidential reason, I would not share any real data here. All code, results, and plots showing below are manipulated already.

