---
hide:
  - toc
---
# Configuration
The backtest has a lot of configurable parameters, which are all defined in the config file ```config.json```. The
standard ```config.json``` looks like this:
```
{
  "exchange": "binance",
  "timeframe": "5m",
  "max-open-trades": 3,
  "starting-capital": 1000,
  "backtesting-from": "2021-03-11",
  "backtesting-to": "2021-03-15",
  "backtesting-till-now": false,
  "stoploss-type": "standard",
  "stoploss": -10,
  "roi": {
    "0": 5,
    "60": 4,
    "120": 3
  },
  "pairs": ["BTC/USDT", "LTC/USDT", "ETH/USDT"],
  "currency": "USDT",
  "fee": 0.25,
  "strategy-name": "MyStrategy",
  "strategies-folder": "strategies",
  "plots": true,
  "mainplot_indicators": ["ema5", "ema21"],
  "subplot_indicators": ["volume"]
}
```
To change something in the configuration, just simply modify the value on the right (after ```"[PARAMETER]":```).

## Parameters
### Exchange
The ```exchange``` that is used to retrieve OHLCV data from. Currently, we only support the ```"binance"``` exchange.

### Timeframe
Timeframe that is used to populate the indicators and buy/sell signals. A ```timeframe``` can be defined by either using 
minutes ```m```, hours ```h``` or days ```d```. We recommend using one of the following timeframes:
```1m```, ```5m```, ```15m```, ```30m``` or ```1h```. 

### Max. open trades
The maximum amount of trades that can be open simultaneously. The engine is designed such that it can only have a 
maximum of one open trade per pair, which means that within all open trades there can never be a duplicate pair. Because
of this restriction buy signals can be rejected, since it could be the case that the pair you want to open a new trade
for has already an open trade.

The ```max-open-trades``` is used to calculate the stake amount for a certain trade. The standard way of calculating the stake 
amount is by:
```
stake-amount = (1 / max-open-trades) * realised-profit
```

But when calculating the stake amount we also have to factor in the amount of trading pairs, since this can influence 
the way that the stake amount is determined. We explain the relation between the max. open trades and amount of trading
pairs in the following three scenarios:

1. **Max. open trades > amount of trading pairs:** because we can never reach the max open trades (not enough trading pairs),
   the value for max. open trades will be set equal to the amount of trading pairs.
   
2. **Max. open trades < amount of trading pairs:** when this occurs certain buy signals can be rejected. Above we 
   described that the engine can not open multiple trades on the same pair. In this scenario it can also happen that a 
   pair that does not have an open trade, wants to open a trade (due to a buy signal) but gets rejected. This happens
   when max. open trades is reached, because then all new buy signals are rejected.
   
3. **Max. open trades == amount of trading pairs:** nothing changes.

### Starting capital
The amount of capital that the bot is able to use for trading.

### Backtesting period
The specified period where the bot will be analysed on. Here, ```backtesting-from``` will indicate the starting point and 
```backtesting-to``` will indicate the ending point of the backtesting period. Both timestamps are defined in the 
```config.json``` as YYYY-MM-DD. 

If you want to test the bot until your current date, you can enable the boolean 
```backtesting-till-now``` by setting its value to ```true```. It will then backtest from the defined 
```backtesting-from``` until your current point in time (specific to the minute).

### Stoploss
When using a stoploss you can use three different types, which can be altered by changing the value for 
```stoploss-type```:
1. ```"standard"```: this stoploss type is activated by default and prevents the bot from dealing with great losses. 
   When this stoploss is selected a trade will close automatically when the profit percentage for that trade is equal to 
   or drops below the configured ```stoploss```.
   
2. ```"trailing"```: this stoploss type enables a trailing stoploss. When using this stoploss type a stoploss value 'SL'
   is calculated at every candle. This SL will indicate the 'sell price' at which a trade needs to be closed. If the 
   traded pair (e.g. BTC/USDT) is equal or drops below this price, the corresponding trade will be closed. SL is 
   calculated at every candle by: ```SL = candle-high * (1 - trailing-percentage)```. 
   - ```candle-high``` is the highest price seen in that specific candle.
   - ```trailing-percentage``` is the stoploss percentage defined by ```stoploss```in the ```config.json```.
   
   The algorithm used for trailing stoploss is defined as follows:
   1. TSL is defined as the SL of first candle
   2. Get SL of next candle
   3. If SL for next candle is HIGHER than TSL:
       - TSL = next candle SL
       - back to Step 2.
   4. If SL for next candle is LOWER than TSL:
       - back to Step 2.
      
3. ```"dynamic"```: stoploss type which can be defined in the strategy class. See ```my_strategy_advanced.py``` for an
   example on how this stoploss needs to be defined. The basic use is that for each candle a stoploss price needs to be
   defined and if the candle-low (lowest seen price in that specific candle) is equal or drops below the defined
   stoploss price, that trade will be closed.
   > Note: if ```stoploss-type``` is set to ```"dynamic"``` but the stoploss function in the strategy class is either
   > undefined or defined wrong, the ```stoploss-type``` will be automatically changed to ```"standard"``` and will use
   > the ```stoploss``` percentage from the ```config.json```.

### ROI
Defines the Return On Investment (```roi```) sell signals. See the 
[Termsheet](https://docs.dematrading.ai/getting_started/trading101/termsheet/#roi) for more information. ROI is used to
close a trade when a certain ROI is reached. In addition, you can also specify after how many minutes the trade should 
be closed. In the ```config.json``` the standard configuration is:
```
"roi": {
    "0": 5,
    "60": 4,
    "120": 3
  }
```
This configuration can be interpreted as: 
- When ROI is equal to 5%, close the trade immediately.
- When ROI is equal to 4%, close the trade after 60 minutes.
- When ROI is equal to 3%, close the trade after 120 minutes.

### Trading pairs
Specifies which pairs you want the bot to trade. Make sure that when specifying the list of ```pairs``` that the base
for each pair needs to be the same and equal to the defined ```currency```.

### Fee
Defines the ```fee``` percentage. This percentage will be applied on every trade entry and exit.

### Strategy
Specifies which strategy to backtest. Make sure the ```strategy-name``` is equal to the name of the strategy class
(not the name of the ```.py``` file). Furthermore, make sure the ```.py``` file that contains the strategy class is 
saved in the ```strategies-folder```.

### Plots
After each backtest there is the possibility to see a plot of the change in price, buy/sell signals (both executed and 
not executed) and indicators. This function is automatically enabled and can be disabled by settings the ```plots``` 
boolean to ```false```. The indicators in the plots can be configured by changing the value for either 
```mainplot_indicators``` and/or ```subplot_indicators```. Make sure when adding new indicators to the list of
plot-indicators, that these indicators are populated in the strategy.
