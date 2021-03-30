# Strategy Mistakes

## Getting Previous Candle
You can access data from previous candle using the following code in both ``buy_signal`` and ``sell_signal``:
````python
index = len(dataframe.index) - 2
previous_candle = dataframe.iloc[index]
````

## Getting MACD values
Getting MACD values could give you some trouble. Therefore, use the example below for configuring MACD in your strategy.
````python
macd = ta.MACD(dataframe)
dataframe['macd'] = macd['macd']
dataframe['macdsig'] = macd['macdsignal']
dataframe['macdhist'] = macd['macdhist']
````
**Advanced configuration:**
````python
macd = ta.MACD(dataframe, fastperiod=10, slowperiod=20, signalperiod=9)
````

## Using .mean()
If you are using .mean() in for example ``dataframe['volume'].mean()`` you should always add the ``.rolling()`` before the .mean, otherwise the average would be based on ALL of the available data from the dataframe. See the code example below:
```python
dataframe['volume'].rolling(14).mean()
```
In this case, we use the last 14 candles to calculate the average volume. 