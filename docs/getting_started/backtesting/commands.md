# Backtesting commands
```

    usage: main.py  [-h] [-cap STARTING_CAPITAL] [-from BACKTESTING_FROM] 
                    [-to BACKTESTING_TO] [-sl STOPLOSS] [-plots PLOTS]
                    [-sl_type STOPLOSS_TYPE] [-c CONFIG] [-s STRATEGY_NAME]
                    {init} ...
    
    positional arguments:
    {init}
    
    optional arguments:
    -h, --help              show this help message and exit
    -cap STARTING_CAPITAL, --starting-capital STARTING_CAPITAL
                            Value of starting capital. 
    -from BACKTESTING_FROM, --backtesting-from BACKTESTING_FROM
                            Specify start date of backtesting period.
    -to BACKTESTING_TO, --backtesting-to BACKTESTING_TO
                            Specify end date of backtesting period.
    -sl_type STOPLOSS_TYPE, --stoploss-type STOPLOSS_TYPE
                            Select stoploss type ('standard', 'trailing', 'dynamic').
    -sl STOPLOSS, --stoploss STOPLOSS
                            Define stoploss percentage (applies for 'standard' and 'trailing' 
                            stoploss).
    -plots PLOTS, --plots PLOTS
                            Create candle data plots. Also includes populated buy/sell signals 
                            and indicators specified in the config.
    -c CONFIG, --config CONFIG
                            Select specific config file.
    -s STRATEGY_NAME, --strategy-name STRATEGY_NAME
                            Select specific strategy.

```
To backtest your created strategy you can make use of these commands.