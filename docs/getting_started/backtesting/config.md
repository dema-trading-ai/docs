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
The ```exchange``` that is used to retrieve OHLCV data from. Currently we only support the ```binance``` exchange.

### Timeframe
Timeframe that is used to populate the indicators and buy/sell signals. A ```timeframe``` can be defined by either using 
minutes ```m```, hours ```h``` or days ```d```. We recommend using the most commonly used timeframes, which is either 
```1m```, ```5m```, ```15m```, ```30m``` or ```1h```. 

### Max. open trades
The maximum amount of trades that can be open simultaneously. The engine is designed such that it can only have a 
maximum of one open trade per pair, which means that within all open trades there can never be a duplicate pair. Because
of this restriction buy signals can be rejected, since it could be the case that the pair you want to open a new trade
for has already an open trade.

The max open trades is used to calculate the stake amount for a certain trade. The standard way of calculating the stake 
amount is by:
```
stake_amount = (1 / max-open-trades) * realised-profit
```
> TODO: definition for realised profit can be found in the Termsheet

But when calculating the stake amount we also have to factor in the amount of trading pairs, since this can influence 
the way that the stake amount is determined. We explain the relation between the max. open trades and amount of trading
pairs in the following three scenarios:

1. **Max. open trades > amount of trading pairs:** when this happens the engine takes the smallest value out of the two 
   and uses that as the max. open trades value.
   
2. **Max. open trades < amount of trading pairs:** when this occurs certain buy signals can be rejected. Above we 
   described that the engine can not open multiple trades on the same pair. In this scenario it can also happen that a 
   pair that does not have an open trade, want to open a trade (due to a buy signal) but gets rejected. This happens
   when max. open trades is reached, because then all new buy signals are rejected. Furtermore, the calculation of the
   stake amount stays the same.
   
3. **Max. open trades == amount of trading pairs:** nothing changes.

### Starting capital
### Backtesting period
### Stoploss
### ROI
### Trading pairs
### Currency
### Fee
### Strategy name
### Strategies folder
### Plots
