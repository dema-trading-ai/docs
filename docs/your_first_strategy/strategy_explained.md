---
hide:
  - toc
---
# Strategy Explained
After installing the Engine, it is time to start working on a strategy of your own. In this chapter you will learn how
to get started with developing your very own strategy. To give you a head start, we have included a sample strategy
which can be found in the file <YOUR_DIRECTORY_NAME>/strategies/my_strategy.py (where you just created the project, as
explained in [Section 1.2: Running](/installation_and_updating/running)). We will use this sample strategy to explain
the main concepts of strategies.

## Generate Indicators

The first function in the 'my_strategy.py' file is the generate_indicators function. This function, like the name
implies, generates indicators, which in turn are used to calculate when to buy, and when to sell. The function looks
like this:

```python
def generate_indicators(self, dataframe: DataFrame, additional_pairs=None) -> DataFrame:
   """
   :param dataframe: All passed candles (current candle included!) with OHLCV data
   :type dataframe: DataFrame
   :param additional_pairs: Possible additional pairs with specified timeframe
   :type additional_pairs: dict
   :return: Dataframe filled with indicator-data
   :rtype: DataFrame
   """
   # RSI - Relative Strength Index
   dataframe['rsi'] = ta.RSI(dataframe, timeperiod=14)

   # EMA - Exponential Moving Average
   dataframe['ema5'] = ta.EMA(dataframe, timeperiod=5)
   dataframe['ema21'] = ta.EMA(dataframe, timeperiod=21)

   return dataframe
```

The sample strategy is based on two indicators: the RSI (Relative Strength Index) and two versions of the EMA
(Exponential moving average): EMA5, which averages over the last 5 timesteps, and EMA21, which averages over the last
21 timesteps.

You probably want to add more indicators on which to base your buy and sell signals, when you start developing your
own strategy - be sure to add them to the dataframe (the collection of data) in the same way as in the code above. For
example, if you want to add SMA5 (Simple Moving Average over the last 5 timesteps), just add the following line before
the ‘return dataframe’ line:

```python
dataframe['sma5'] = ta.SMA(dataframe, timeperiod=5)
```

For more examples of indicators and how to use them, you can take a look at the file
<YOUR_DIRECTORY_NAME>/strategies/indicator_sample.py - a large amount of indicators is shown there. Just take your
pick, and copy the (uncommented) line to your strategy file.

!!! attention
    If you use an indicator with a large amount of timesteps necessary, beware: if the indicator needs more timesteps than
    there are candles in your dataset, you will get errors or distorted results. Please make sure your timeframe is
    sufficiently small, and your backtesting period is sufficiently large, so you have enough candles in your backtest
    to base your indicators upon. For more information about how to configure the timeframe and backtesting period, see
    [Section 2.4: Editing your configuration](/your_first_strategy/editing_your_configuration).


!!! note
    If you use a TA-Lib function (any ta.FUNCTION_HERE function, like the RSI, EMA, and SMA used above) be sure to include a ‘timeperiod’ explicitly, otherwise it will be set to a default timeperiod of two weeks. So be sure to change this:
    ```python
    dataframe['rsi'] = ta.RSI(dataframe)
    ```
    To this:
    ```python
    dataframe['rsi'] = ta.RSI(dataframe, timeperiod=14)
    ```

## Buy Signal
In order for your strategy to buy crypto, you will need to generate ‘buy signals’. These signify points where you want
your strategy to buy. These are usually based on the indicators; when they reach a certain condition, a buy signal
should be generated. In the sample strategy file, the function to generate buy signals looks like this:

```python
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
           (dataframe['rsi'] < 30) &
           (dataframe['ema5'] < dataframe['ema21']) &
           (dataframe['volume'] > 0)
       ),
       'buy'] = 1

   # END STRATEGY

   return dataframe
```

This code generates a buy signal (buy = 1) for every timestep where the rsi is below 30, and the ema5 is below the
ema21. The last line, volume > 0, means that you should only generate a buy signal when there is volume, ergo when
trades are actually being made. While you are encouraged to change the other buy conditions, you should keep the
volume condition in your strategy! You can change the conditions by removing and/or adding lines. Keep in mind that
a buy signal only translates into an actual buy if your algorithm is not already in position, and if there is enough
open budget left to open a trade with.

## Sell Signal
The function to generate the sell signal is very similar to the buy_signal function. The function generates points on
which you want your algorithm to sell. The code looks as follows:

```python
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
           (dataframe['rsi'] > 70) &
           (dataframe['volume'] > 0)
       ),
       'sell'] = 1

   # END STRATEGY

   return dataframe
```

In this sample strategy, a sell signal is generated whenever the RSI indicator goes above the value of 70. Keep in
mind that a sell signal only translates into an actual sell if the algorithm is already in position - if it hasn’t
bought first, it cannot sell!

!!! note
    Apart from a generated sell signal, positions can also be closed (sold) by a triggered Stoploss or ROI (Return on
    Investment). These can be set in your configuration file, and will be discussed more thoroughly in the
    [Section 2.3: Editing the Stoploss and ROI](/your_first_strategy/stoploss_and_roi).