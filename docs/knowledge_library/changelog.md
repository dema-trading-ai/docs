# Changelog

## Version 0.7
***
Stable beta release with added features:

- Complete redesign of backtesting results overview
- BTC and ETH as base pairs
- Open and Closed Trades log
- Shortest / average / longest trade duration statistic
- Changed the OHLC plots from bars to candlesticks
- Improved download speed of candles from exchanges
- Better and timelier logging of engine functionality
- Improved max seen drawdown and max realised drawdown
- Additional Pairs
- Improved data loading speed
- Improved plotting speed
- Buy & Hold Drawdown statistic
- Winning weeks statistic
- Portfolio equity plot
- (Experimental) Hyperparameter optimization
- (Experimental) Self contained executables & installers

## Version 0.6
***
Stable beta release with added features:

- Rigorous testing and improvement of all current statistics
- Refactoring of the entire engine
- Improvement of plot readability
- Improvement of Realized Drawdown & Seen Drawdown statistic
- Average numbers of trades per day

## Version 0.5
***
Stable beta release with added features:

- Fixed wrong avg trade duration
- Changed the way 'spend_amount' (trade value for new trade) is defined. This will prevent the portfolio from becomming unbalanced (e.g. 1/4 budget in one trade and 3/4 budget in another trade)
- Old: (1 / available_spaces) * budget
- New: (1 / amount_of_pairs) * budget 
- Fixed incorrect drawdown calculations for 'backtest results' 
- Fixed incorrect drawdown calculations for 'per coin insights'
- Changed profit percentage columns for 'per coin insights'
- Now consists of 'avg profit', 'cum profit' and 'total profit'
- Profit percentages only include closed trades and not open trades (these are shown in 'left open trades' table)
- Renamed metrics in results table:
- Max drawdown bad trade train -> most consecutive losses
- Most drawdown 1 trade -> Worst trade
- Seen drawdown from -> Max seen drawdown from
- Seen drawdown to -> Max seen drawdown to
- [Removed] Max drawdown trades
- Added average marketchange of BTC and whitelisted coins
- Fixed incorrect use of downloaded .json data
- Updated dynamic stoploss warning
- Changed plots argument to boolean
- Removed if statement from advanced_strategy

## Version 0.4
***
Stable beta release with added features:

- Several bugfixes
- Enhanced backtesting overview 
- Added plotting possibilities 
- Added Dynamic- and Trailing stoploss 
- Added QtpyLib 
- Development Image Publishing pipeline
- Added CLI support

## Version 0.3
***
Stable beta release with added features:

- 140% decrease of backtest time.
- docker-compose file with proper volume mounting
- new progress bars
- checks for missing ticks
- small optimizations
- moved docs to separate repository
- dynamic stoploss

## Version 0.2
***
Stable beta release with added features:

- Added fee-support
- Improved overall results overview
- Improved documentation

## Version 0.1
***
First release including features:

- Easy strategy customization
- OHLCV data in dataframe
- Release / test pipelines
- Progress bar for time indication
- Enhanced backtest results
- Automatically downloading data
- Configurable base currency
- Documentation setup
- Dockerized the whole engine