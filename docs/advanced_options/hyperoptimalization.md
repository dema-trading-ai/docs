# [experimental] Hyperparameter optimization

## Usage
`engine --alpha-hyperopt=true`

Example strategy:
```python

# Mandatory Imports
import talib.abstract as ta
from pandas import DataFrame
from backtesting.strategy import Strategy
from modules.public.hyperopt_parameter import integer_parameter, float_parameter
from modules.public.trading_stats import TradingStats


class MyStrategy(Strategy):
    # parameters
    buy_rsi = integer_parameter(default=40, low=10, high=50, step=1)
    sell_rsi = float_parameter(default=70., low=60., high=80., step=1.)
    
    def generate_indicators(self, dataframe: DataFrame, additional_pairs=None) -> DataFrame:
        dataframe['rsi'] = ta.RSI(dataframe, timeperiod=14)
        dataframe['ema5'] = ta.EMA(dataframe, timeperiod=5)
        dataframe['ema21'] = ta.EMA(dataframe, timeperiod=21)

        return dataframe

    def buy_signal(self, dataframe: DataFrame) -> DataFrame:
        dataframe.loc[
            (
                    (dataframe['rsi'] < self.buy_rsi) &
                    (dataframe['ema5'] < dataframe['ema21']) &
                    (dataframe['volume'] > 0)
            ),
            'buy'] = 1

        return dataframe

    def sell_signal(self, dataframe: DataFrame) -> DataFrame:
        dataframe.loc[
            (
                    (dataframe['rsi'] > self.sell_rsi) &
                    (dataframe['volume'] > 0)
            ),
            'sell'] = 1

        return dataframe
        
    # LOSS function
    def loss_function(self, stats: TradingStats):
        winning_trades = len(list(filter(lambda trade: trade.profit_ratio > 1., stats.trades)))
        avg_profit = sum(map(lambda trade: trade.profit_ratio, stats.trades)) * 100.
        amount_of_trades = len(stats.trades)
        if amount_of_trades == 0:
            return 1.
        win_ratio = winning_trades / amount_of_trades
        return -avg_profit * win_ratio


```

### Parameters
#### integer_parameter()
```python
buy_rsi = integer_parameter(default=40, low=10, high=50, step=1)
```

Defines integers within a specified range. The boundaries of this range are defined by the 
```low``` and ```high``` parameters and the step size by the ```step``` parameter. During hyper-opt 
all the defined integer values will be 'tested' and the value where the ```loss_function()``` is 
**minimal** (in combination with other hyper-opt parameters) will be presented after the 
hyper-opt is 
finished. 

When ```integer_parameter()``` is used but hyper-opt is not enabled through the command line, the 
engine will use the defined ```default``` value.
> Note: make sure that when using a parameter function, that these variables are used when 
> populating the buy/sell signals (see example strategy above)

#### float_parameter()
```python
sell_rsi = float_parameter(default=70., low=60., high=80., step=1.)
```

Defines floats within a specified range. Works similar to ```integer_paramater()``` except that 
```float_parameter()``` uses floats instead of integers. This allows the hyper-opt to be able to 
find a more precise optimal value.

### Loss function
```python
def loss_function(self, stats: TradingStats):
        winning_trades = len(list(filter(lambda trade: trade.profit_ratio > 1., stats.trades)))
        avg_profit = sum(map(lambda trade: trade.profit_ratio, stats.trades)) * 100.
        amount_of_trades = len(stats.trades)
        if amount_of_trades == 0:
            return 1.
        win_ratio = winning_trades / amount_of_trades
        return -avg_profit * win_ratio
```
Calculation method used for finding the loss. Goal of the hyper-opt is to **minimize** the loss 
calculated in this function. The calculation method can be changed to hyper-opt with another 
type of loss, but we recommend using this implementation. 
