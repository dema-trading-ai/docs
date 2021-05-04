# Configuring your backtest

## Configuration

In the ``config.json`` file you will find all necessary and important configuration options.
***
## ROI

The ROI table in the configuration is used to sell at a certain percentage of profit after a defined time. The `keys` in the dictionary are in minutes, the `values` are the percentages. Keys should always be an `int` (round number) with double quotes. Value could be an `int`(round number) or a `float` (with decimals).

```json
   "roi": {
     "0": 5,
     "60": 4,
     "120": 3.5
   }
```

This configuration means positions will always be closed if the profit is higher than 5%. After an hour (60 minutes) the position will automatically be closed if the profit is higher than 4%. Even the smallest change in the ROI could mean a huge difference when it comes to profit.
***
## Stop loss
### How to use 'Stop Loss'

A Stop-Loss is an advanced order that is used by traders that limits any form of additional losses. When a specific price is met, the order is triggered.

An example would be that buying in at 100 would stop any form of losses at 95. In this case the stop-loss treshold would be -5%. Similarly, it can be done for a profit where one can set it to +5%, which in turn would mean the profit would be capped at 105.

This in itself can be modified in any increment.
The stoploss (SL) function is to prevent extreme loses. The SL value in the configuration file could be a `float`(with decimals) or an `int`(round number).

```json
   "stoploss": "-0.5",
```

This configuration means positions will always be closed if the profit is lower than -0.5%.

### Custom Stop loss

Alternatively, currently we have 3 options in terms of stop loss configurations.

```json
  {
    "name": "stoploss-type",
    "default": "standard",
    "options": ["standard", "trailing", "dynamic"],
    "type": "string",
    "cli": {
      "short": "sl_type"
    }
  }
```
As seen in the code above, these three consists out of the following:

- 'standard' -> standard stoploss calculation based on the price when opening a trade (requires 'stoploss' percentage)
- 'trailing' -> trailing stoploss function (requires 'stoploss' percentage)
- 'dynamic' -> configurable stoploss function that can be changed in my_strategy_advanced.py

In the advanced_strategy.py file an example can be seen in terms of the 'dynamic' stop loss; the snippet of code underneath is what you'd find in the file. Following the presented code, you'll be able to implement a dynamic stop loss.

```python
def stoploss(self, dataframe: DataFrame) -> DataFrame:
        """
        Override this method if you want to dynamically change the stoploss 
        for every trade. If not, the stoploss provided in config.json will
        be returned.
        IMPORTANT: this function is only called when in the config.json "stoploss-type" is:
            ->  "stoploss-type": "dynamic"
        :param dataframe: dataframe filled with indicators from generate_indicators
        :type dataframe: Dataframe
        :return: dataframe filled with dynamic stoploss signals
        :rtype: DataFrame
        """
        # BEGIN STRATEGY

        dataframe['stoploss'] = dataframe['ema5']

        # END STRATEGY
```
***
## OHLCV
OHLCV, also known as:

- **O**pen
- **H**igh
- **L**ow
- **C**lose
- **V**olume

Can be used to trade in an easy fashion. A simple example for this would be by using the close. The close is the end value of the current candle, where it closes and goes into a new candle.

```python
dataframe.loc[
    (
        (dataframe['close'] < 50)
    ),
    'buy'] = 1
```
Which means you'll buy an asset when the close is below 50. This can be adjusted as you see fit, however, the general jist of it is that all the OHLCV can be used in a similar fashion.
***
## How to use 'if statements with candles' and elucidating timeframes

When generating your indicators, ensure that what you type down makes sense. For example:

```python
if current_candle['close'] > current_candle['ma200']:
```

Will result in an error due to the fact that the candle will be marked as close yet it is supposed to surpass the past 200 point timeframe average.

A correct example on how to use an if statement would be:

```python
if int(timestamp) > time:
                ohlcv = data_dict[timestamp]
```

Or

```python
dataframe.loc[
    (
        (dataframe['ma10'] < dataframe['ma100'])
    ),
    'buy'] = 1
```

Albiet, the latter is already a timeframe module and would already be a part of a possible strategy. 

Changing the timeframe can make a huge difference; if you apply a short timeframe and put it up against a large timeframe as presented in the second example, you can detect shorts and act on them!

***
## Getting started

Now you've seen how we configured all the basic settings and buy/sell signals. From now on, you can start working on **your very own trading algorithms**. More information regarding this can be found on the strategies page.

