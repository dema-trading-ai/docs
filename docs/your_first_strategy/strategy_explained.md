---
hide:
  - toc
---
# Developing a strategy
On this page you will learn how to get started with developing your very own strategy. To give you a headstart, we included a sample strategy which can be found in ``/strategies/my_strategy.py``. 
***
## Sample strategy
How does our sample strategy work? We will guide you through the process. The sample can be found in ``/strategies/my_strategy.py``. 

!!! attention
    Not all settings in this file need to be present. You can leave out, add, or change certain signals. This mostly pertains to the configurable parts; you can alter them, change them, and freely work around them as you please.

### Generate indicators
To be able to base our buy / sell signal on indicators, we need to generate these strategies. 

For this strategy we decided we want to use RSI and EMA indicators to trigger buys/sells. We can make the calculated value available to the buy/sell methods by adding it to the dataframe. Like this for example: 
``dataframe['rsi'] = ta.RSI(dataframe)``

!!! attention
    Setting this to something other than the maximum span of candles used will result in distorted results or errors.

!!! note
    When creating a strategy, make sure to include a 'timeperiod' in all of the TA-Lib functions. This means that you should turn 
```python 
   dataframe['rsi'] = ta.RSI(dataframe)
```
into:
```python
   dataframe['rsi'] = ta.RSI(dataframe, timeperiod = 14)
```

### Buy signal
In our buy signal, we set some conditions for our signal. In our implementation, the pair wil only be bought when all of the following conditions are true.
```python
current_candle['rsi'] < 30
current_candle['ema5'] < current_candle['ema21']
current_candle['volume'] > 0
```

### Sell signal
In our sell signal, we set some conditions for our signal. In our implementation, the pair wil only be sold when all of the following conditions are true. Beside the sell signal, positions can be closed using the [Stop Loss](#stop-loss) or [Return on Investment](#ROI) configurations in the ``config.json`` file.
```python
current_candle['rsi'] > 70
current_candle['volume'] > 0
```

### Minimum candles 
On the top of ``my_strategy.py``, ``min_candles`` is defined. This is used as an offset for the amount of candles needed to calculate the biggest indicator. In our case, EMA(21) needs atleast 21 candles to work properly. Therefore, we set ``min_candles`` to 21. 

### Configuration
In the ``config.json`` file you will find all necessary and important configuration options. 
#### ROI
The ROI table in the configuration is used to sell at a certain percentage of profit after a defined time. The `keys` in the dictionary are in minutes, the `values` are the percentages. Keys should always be an `int` with double quotes. Value could be an `int` or a `float`.
```json
  "roi": {
    "0": 5,
    "60": 4,
    "120": 3.5
  }
```
This configuration means positions will always be closed if the profit is higher than 5%. After an hour (60 minutes) the position will automatically be closed if the profit is higher than 4%.

#### Stop loss
The stoploss (SL) function is to prevent extreme losses. The SL value in the configuration file could be a `float` or an `int`.
```json
  "stoploss": "-0.5",
```
This configuration means positions will always be closed if the profit is lower than -0.5%.

## Getting started
Now you've seen how we configured all the basic settings and buy/sell signals. From now on, you can start working on **your very own trading algorithms**. This guide will use a very simple method of finding the right indicators and using them in your strategy. 

!!! note 
    Creating your own strategy might take some time. Don't give up too fast! [On the bottom of the page](#extra-information) we listed some reading and learning material to become more familiar with trading, coding and everything else.
    
### Finding indicators
1. Go to [TradingView](https://www.tradingview.com/chart/)
2. Select a view of any coin pair you're interested it (make sure to select 'cryptos').
3. Have a look at the graph and decide at what moments you'd like to buy / sell.
4. Add some indicators to the graph.
5. See whether the indicators could indicate your buy/sell positions.
6. If you found some sort of pattern, go to the next step.
 
### Configuring indicators
You can have a look at the `indicator_sample.py` file under the `strategies` directory on how to configure indicators for your strategy. 

In this file, we have compiled a large amount of TradingView indicators along with the required `int` (whole numbers). The only thing you'd have to add yourself besides the presented code that contains the indicator you wish to use, is to add a time period within the brackets to ensure that there's a scope in time during which you want to perform the backtest. 
### Using indicators in sell/buy signal
Have a look at the [sell signal](#sell-signal) or [buy signal](#buy-signal) part of the sample strategy. Other python logic and external packages could be applied to the buy/sell signal, as long as it's a condition. 

This means, we can also use the following:
```python 
current_candle.loc[
    (
            ((current_candle['rsi'] < 30) | (current_candle['rsi'] > 40)) &
            (current_candle['ema5'] < current_candle['ema21']) &
            (current_candle['volume'] > 0)
    ),
    'buy'] = 1
```
In this case, a position opens when RSI is either below 30 **or** above 40. 

### Configuring Stoploss / Return On Investment
Stoploss and ROI are really important when creating an algorithm. These will make sure you get the best from your strategy, while not putting everything at risk.

