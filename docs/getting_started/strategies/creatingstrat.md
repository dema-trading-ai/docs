# Creating your first strategy
***
!!! note
    When creating a strategy, make sure to include a 'timeperiod' in all of the talib functions. This means that you should turn 
```python 
dataframe['rsi'] = ta.RSI(dataframe)
```
into:
```python
dataframe['rsi'] = ta.RSI(dataframe, timeperiod = 14)
```

