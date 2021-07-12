# Backtesting arguments
```

    usage: docker-compose run --rm dema-engine  [-h] 
                                                [-cap STARTING_CAPITAL] 
                                                [-from BACKTESTING_FROM] 
                                                [-to BACKTESTING_TO] 
                                                [-sl STOPLOSS] 
                                                [-plots PLOTS]
                                                [-sl_type STOPLOSS_TYPE] 
                                                [-c CONFIG] 
                                                [-s STRATEGY_NAME]
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
When backtesting your created strategy you can make use of the arguments listed above. To run the engine using these 
arguments we have to use ```docker-compose run``` instead of ```docker-compose up```. The command will then look like 
this:
```
docker-compose run --rm dema-engine <command> <optional arguments>
```
> Adding the flag ```--rm``` will remove the container after the backtest is done (highly recommended).

## Examples
### Backtesting period
When you want to configure the backtesting period, you can use the arguments ```-from``` and ```-to```. For both 
arguments the date has to be formatted either YYYYMMDD or YYYY-MM-DD. If the date is not specified in the command line, 
the engine will use the dates in the config. For example, to run a backtest from 2021-01-01 to 2021-02-01 use the 
command:
```
docker-compose run --rm dema-engine -from 2021-01-01 -to 20210201
```
> Here, you can see that the format of the timestamp can be used interchangeably.


### Strategy and config
When working on multiple strategies at the same time it is recommended to use the argument ```-s``` to easily backtest 
another strategy. Make sure your strategies are saved in the ./strategies/ folder and that the classes have different
names. For example, to run a strategy where the class is called 'NewStrategy', use the command:
```
docker-compose run --rm dema-engine -s NewStrategy
```

Furthermore, if each strategy also has its own optimised config you can easily select this as well using the argument 
```-c```. The value for this argument is the path to your new config. If you have saved a new config file in your 
```dema-engine``` folder and called it e.g.```new-strategy-config.json```, you can use the following command:
```
docker-compose run --rm dema-engine -s NewStrategy -c new-strategy-config.json
```





