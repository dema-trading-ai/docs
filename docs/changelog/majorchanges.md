# Overview of all major changes per version

## v0.5 - v0.6
- Fixed several bugs in the profit calculation
- Fixed stoploss not triggering bug
- Fixed roi not triggering bug
- Plot readability improved
- Improved realized and seen drawdown calculation
- Improved marketchange calculation


## v0.4 - v0.5
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

## v0.3 - v0.4
- Several bugfixes
- Enhanced backtesting overview 
- Added plotting possibilities 
- Added Dynamic- and Trailing stoploss 
- Added QtpyLib 
- Development Image Publishing pipeline
- Added CLI support

## v0.2 - v0.3
- 140% decrease of backtest time.
- docker-compose file with proper volume mounting
- new progress bars
- checks for missing ticks
- small optimizations
- moved docs to separate repository
- dynamic stoploss

## v0.1 - v0.2
- Easy strategy customization
- OHLCV data in dataframe
- Release / test pipelines
- Progress bar for time indication
- Enhanced backtest results
- Automatically downloading data
- Configurable base currency
- Documentation setup
- Dockerized the whole engine
- Fee support
- Documentation additions
