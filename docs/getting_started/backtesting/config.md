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

## Parameters
### Exchange
### Timeframe
### Max open trades
### Starting capital
### Backtesting period
### Stoploss`
### ROI
### Pairs
### Currency
### Fee
### Strategy name
### Strategies folder
### Plots