# Strategy Mistakes

## Getting Previous Candle
You can access data from the previous candle using ``.shift(1)``:
````python
previous_candle = dataframe['close'].shift(1)
````

## Getting MACD values
Some indicators return multiple values. This means that you have to 'unpack' the results of that indicator. See the example
below, demonstrated with MACD.
````python
macd = ta.MACD(dataframe)
dataframe['macd'] = macd['macd']
dataframe['macdsig'] = macd['macdsignal']
dataframe['macdhist'] = macd['macdhist']
````

### Setting custom indicator values
Many indicators use default values for certain parameters. However, you can overwrite these values to obtain the desired
behaviour. See below for an example using MACD.
````python
macd = ta.MACD(dataframe, fastperiod=10, slowperiod=20, signalperiod=9)
````
Check the [TA-Lib documentation](https://mrjbq7.github.io/ta-lib/func_groups/momentum_indicators.html) for an overview of 
all indicators, their parameters and their default values.

### Using .mean()
If you are using .mean() in for example ``dataframe['volume'].mean()`` you should always add the ``.rolling()`` before the .mean, otherwise the average would be based on ALL of the available data from the dataframe. See the code example below:
```python
dataframe['volume'].rolling(14).mean()
```
In this case, we use the last 14 candles to calculate the average volume. 