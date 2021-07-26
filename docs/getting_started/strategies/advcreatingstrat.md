# Advanced Algorithm Creation


## Custom Indicators
!!! note "Looking for a specific indicator?"
    Refer to [this](https://github.com/dema-trading-ai/engine/blob/main/modules/setup/config/technical_indicators.py) file for an up-to-date list of custom-coded indicators.

Renowned packages such as Talib and qtpylib provide a wide range of technical analysis tools. However, sometimes a specific
indicator is missing. This often results in custom-coded indicators, based on their formal definitions. 
These custom indicators are collected and made available to all users of the Engine. The aim is to constantly complement
the list. We also encourage users that coded their own indicators to contribute to this collection.

***

### Example
To use the indicators, import the corresponding file at the top of your strategy file:
```python
from modules.setup.config import technical_indicators as indicator
```

Call the desired method in the `generate_indicators()` function like so:
```python
# Ichimoku Cloud
ichimoku_cloud = indicator.ichimoku_cloud(dataframe, conversion_length=9, base_line_length=26, lead_length=52, displacement=26)
dataframe['ichi_conversion'] = ichimoku_cloud[0]
dataframe['ichi_base_line'] = ichimoku_cloud[1]
dataframe['ichi_lead_line1'] = ichimoku_cloud[2]
dataframe['ichi_lead_line2'] = ichimoku_cloud[3]
```