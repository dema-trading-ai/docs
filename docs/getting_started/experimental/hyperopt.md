# [experimental] Hyperparameter optimization

## Usage
`engine --alpha-hyperopt=true`

``` python

# Mandatory Imports
import talib.abstract as ta
from pandas import DataFrame
from backtesting.strategy import Strategy
from modules.public.hyperopt_parameter import integer_parameter, float_parameter
from modules.public.trading_stats import TradingStats


class MyStrategy(Strategy):
    # parameters
    buy_rsi = integer_parameter(40, low=10, high=40)
    sell_rsi = float_parameter(70., low=60., high=80., step=1.)
    
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