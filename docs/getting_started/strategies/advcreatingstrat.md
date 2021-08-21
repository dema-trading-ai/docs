# Advanced Algorithm Creation
***
## Additional pairs

The additional pairs functionality allows you to have candle data available for other coins and timeframes,
other than the current iteration of the run. This allows for more advanced strategies that take the broader
market conditions into account.

To use this functionality, the `additional_pairs()` function needs to be defined in your strategy class. A `("coin", "timeframe")`
formatting is expected. See the code snippet below for an example, which defines that the 4h candle data of BTC/USDT needs to be available 
in the `generate_indicators()` function. More combinations in the tuple formatting can be added, separated by commas.
Note that each combination requires fetching the candle data, and thus might impact performance speed.

!!! note "Multiple timeframes for the same coin?"
    We recommend using only one timeframe per coin, and resampling upwards to achieve longer timeframes.

```python
@staticmethod
def additional_pairs():
    """
    Specify The additional pairs in tuple format; ("pair", "timeframe"), separated by commas.
    :return: list
    """
    return [
        ("BTC/USDT", "4h")
    ]
```
***

Next, the `generate_indicators()` function needs to be modified.  

Firstly, a new argument is required, which makes the above specified coin/timeframe combinations available in a variable.
```python
def generate_indicators(self, dataframe: DataFrame, additional_pairs) -> DataFrame:
```

Secondly, extract the pair from the variable. `add_btc_data` is a DataFrame, containing the usual OHLCV columns:
```python
# Select the BTC/USDT pair from the additional_pairs dictionary
add_btc_data = additional_pairs['BTC/USDT']
```

Next, add indicators to the DataFrame in the traditional way:
```python
# Add your indicators like usual
add_btc_data['rsi'] = ta.RSI(add_btc_data, timeperiod=14)
```

Finally, the DataFrame created above needs to be joined with the original `dataframe`, such that it can be used in the signal functions:
```python
# Finally merge the additional btc data with the standard dataframe.
# The new column will have the following format: ['<column>_<pair>_<timeframe>']
dataframe = self.join_additional_data(dataframe, add_btc_data, self.timeframe, "4h")
```

***
### Full Example
Below is a full example of the usage of the additional pairs functionality.
```python
class MyStrategyAdvanced(Strategy):
    """
    This is an example custom strategy for advanced users, that inherits from the main Strategy class
    """
    @staticmethod
    def additional_pairs():
        """
        Specify The additional pairs in tuple format; ("pair", "timeframe")
        :return: list
        """
        return [
            ("BTC/USDT", "4h")
        ]

    def generate_indicators(self, dataframe: DataFrame, additional_pairs) -> DataFrame:
        """
        :param dataframe: All passed candles (current candle included!) with OHLCV data
        :type dataframe: DataFrame
        :param additional_pairs: Possible additional pairs with specified timeframe
        :type additional_pairs: dict
        :return: Dataframe filled with indicator-data
        :rtype: DataFrame
        """
        # Select the BTC/USDT pair from the additional_pairs dictionary
        add_btc_data = additional_pairs['BTC/USDT']
        # Add your indicators like usual
        add_btc_data['rsi'] = ta.RSI(add_btc_data, timeperiod=14)
        # Finally merge the additional btc data with the standard dataframe.
        # The new column will have the following format: ['<column>_<pair>_<timeframe>']
        dataframe = self.join_additional_data(dataframe, add_btc_data, self.timeframe, "4h")
        
        # EMA - Exponential Moving Average
        dataframe['ema50'] = ta.EMA(dataframe, timeperiod=50)
        dataframe['ema200'] = ta.EMA(dataframe, timeperiod=200)

        return dataframe

    def buy_signal(self, dataframe: DataFrame) -> DataFrame:
        """
        :param dataframe: Dataframe filled with indicators from generate_indicators
        :type dataframe: DataFrame
        :return: dataframe filled with buy signals
        :rtype: DataFrame
        """
        # BEGIN STRATEGY
        dataframe.loc[
            (
                (
                    (dataframe['ema50'] > dataframe['ema200']) &
                    (dataframe['fastd'] > dataframe['fastk']) &
                    (dataframe['volume'] > dataframe['volume'].rolling(200).mean() * 4) &
                    (dataframe['rsi'] > 50)
                )
                 &
                (dataframe['rsi_BTC/USDT_4h'] < 30)     # additional pair usage
            ),
            'buy'] = 1
        # END STRATEGY
        
        return dataframe
    
    def sell_signal(self, dataframe: DataFrame) -> DataFrame:
        """
        :param dataframe: Dataframe filled with indicators from generate_indicators
        :type dataframe: DataFrame
        :return: dataframe filled with sell signals
        :rtype: DataFrame
        """
        # BEGIN STRATEGY
        dataframe.loc[
            (
                # BULL MARKET
                (dataframe['ema50'] > dataframe['ema200']) &
                (dataframe['rsi'] > 60) &
                (dataframe['macd'] < 0) &
                (dataframe['minus_di'] > 0)
            
            ),
            'sell'] = 1
        # END STRATEGY
        
        return dataframe
```
***

## Custom Indicators
!!! note "Looking for a specific indicator?"
    Refer to [this](https://github.com/dema-trading-ai/engine/blob/main/modules/setup/config/technical_indicators.py) file for an up-to-date list of custom-coded indicators.

Renowned packages such as Talib and qtpylib provide a wide range of technical analysis tools. However, sometimes a specific
indicator is missing. This often results in custom-coded indicators, based on their formal definitions. 
These custom indicators are collected and made available to all users of the Engine. The aim is to constantly complement
the list. We also encourage users that coded their own indicators to contribute to this collection.

***

### Example
To use the indicators, import the corresponding file at the top of your strategy file:
```python
from modules.public import technical_indicators as indicator
```

Call the desired method in the `generate_indicators()` function like so:
```python
# Ichimoku Cloud
ichimoku_cloud = indicator.ichimoku_cloud(dataframe, conversion_length=9, base_line_length=26, lead_length=52, displacement=26)
dataframe['ichi_conversion'] = ichimoku_cloud[0]
dataframe['ichi_base_line'] = ichimoku_cloud[1]
dataframe['ichi_lead_line1'] = ichimoku_cloud[2]
dataframe['ichi_lead_line2'] = ichimoku_cloud[3]
```