# Frequently Asked Questions

## Why is the default fee set at 0.25%
The default value of the fee is 0.25% for both entries and exits. That means a round trip for a trade (buy and sell) 
costs 0.5%. This value accounts for higher commissions on 3rd partner platforms and exchanges. Backtesting will therefore 
more closely resemble a live trading environment.
***
## How do I disable ROI or SL?
Currently there is no 'toggle'. However, you can still achieve the same results by giving those settings an unrealistic high value.
Essentially, there are disabled in that case, as they will never trigger.