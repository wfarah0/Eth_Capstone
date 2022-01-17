# Ethereum prediction capstone \\ "When should I buy or sell Ethereum?"

*Ethereum is a crypto asset created by Vitalik Buterin in 2016 that has seen an astronomical explosion in value over the last two years (over 500%) 
placing it next to bitcoin as the second major crypto asset on the market. But much like bitcoin, its price fluctuations can be erratic, and therefore difficult to predict. 
While the traditional wisom for crypto trading has been to "buy and hold" this project attempts to model Ethereum's price movements to a degree that allows us to pinpoint optimal buy/sell/hold positions so as to optimize our long term profits.*

## DATA

The data for this project was obtained from cryptodatadownload.com. It is a historical dataset of Ethereum prices on the crypto marketplace known as 'Binance' ranging from August 2017
to December 2021. 


## CLEANING
Can be found [HERE](https://github.com/wfarah0/Eth_Capstone/blob/main/cleanEth.ipynb)

Cleaning for the dataset was relatively simple. I only had to remove the unix timecodes, make sure the dates were in datetime format, and ensure no data was missing.

![cleaned data](https://github.com/wfarah0/Eth_Capstone/blob/main/dat.PNG)

## EDA
Can be found [HERE](https://github.com/wfarah0/Eth_Capstone/blob/main/ExploringEth%20(1).ipynb)

-Firstly I created a 'return' column in my dataframe to observe how percentage change in price correlated with the rest of the dataset

-Secondly I created a correlation heatmap using seaborn 

![heatmap](https://github.com/wfarah0/Eth_Capstone/blob/main/heatmp.PNG)
We can see that Volume of Ethereum traded tends to correlate the strongest with price. 


## ML MODELING
Can be found [HERE](https://github.com/wfarah0/Eth_Capstone/blob/main/RF_eth_modeling_ft_backtest%20(1).ipynb)

Initially I attempted an Autoregressive Integrated Moving Average model (ARIMA) similar to how one would model a market equity. This proved unsuccessful, as crypto assets behave 
in a much less predictable fashion, and tend to resist mean regression in the short term as well as long term. 

Thus I shifted my strategy to a RandomForestRegression model.

-This involved creating a rolling window in which our RandomForestRegressor would create and plot a series of lagged variables which would serve as our features. 
![features](https://github.com/wfarah0/Eth_Capstone/blob/main/features_pt1.PNG)

![plotted](https://github.com/wfarah0/Eth_Capstone/blob/main/features_pt2.PNG)
-We then put these features once again through our model to determine the strength of their predictive power. 
![strength](https://github.com/wfarah0/Eth_Capstone/blob/main/features_pt3.PNG)

### FORECASTING

-Now we can apply our strongest feature to the model and attempt to predict
![forecast](https://github.com/wfarah0/Eth_Capstone/blob/main/frcast.PNG)
-We creat a split between out training and test data. 

-Training goes from start to August 2021. Test is August 2021 to December 2021.
![pt2](https://github.com/wfarah0/Eth_Capstone/blob/main/frcast_pt2.PNG)
-We end with a mean squared error of 10.674
![mse](https://github.com/wfarah0/Eth_Capstone/blob/main/mse.PNG)

While not a great model for predicting longterm growth, we see that in the test period several dip and rise locations are
accurately predicted, albeit on a far smaller magnitude. These dips the model predicts will be our'buy' signals in our trading 
strategy, with the peaks being our 'sell' signals. 

![sig](https://github.com/wfarah0/Eth_Capstone/blob/main/sig.PNG)


## BACKTESTING
-This backtest was a daytrading simulation using our our test predictions. 
![test](https://github.com/wfarah0/Eth_Capstone/blob/main/btest.PNG)

-While we did make a thousand or so dollars, we made a few thousand less than had we just held at our initial 'buy in' period. 
![testpt2](https://github.com/wfarah0/Eth_Capstone/blob/main/btest_pt2.PNG)
## Conclusion
Despite our backtesting informing us that our current model does not have the ability to successfully daytrade, it **does** sucessfully safe entry and exit points
for Ethereum investing compared to blind guessing. 

**Consider** that in the months of August, September, and October (when ETH was on the downswing) our model **correctly** identifies price floors on 08/13, 09/11/, and 10/19. 
So while I cannot recommend day trading, the model proves intself useful in providing insight on whether one should enter, or hold off on entering a long term position. 
