---
hide:
  - toc
---

# Running

Once you have successfully installed the Engine, it is time to run it. Open a terminal (MacOS) or Powershell (with
administrator rights) (Windows), and execute the following commands.

To create your project in a new folder, use the following command:
```
engine init <YOUR_DIRECTORY_NAME>
```

Move to the directory you just created with the following command:
```
cd <YOUR_DIRECTORY_NAME>
```

Then, to run the Engine, simply execute the following command:
```
engine
```

Once you have done so, the Engine will run with a sample strategy. The results of the backtest will appear on your
screen. A detailed explanation of the results can be found in
[Section 2.3: Results explained](/your_first_strategy/results_explained).

## Advanced Running Options
There are multiple parameters you can add on to the executable command, in order to customize the running of the Engine.
Here is a short overview of all possibilities.

- Display the overview of all possible parameters of the engine:
```
engine -h
```

- Set the starting capital to 500:
```
engine -cap 500
```

- Set the backtesting from date to 14th of October 2020:
```
engine -from "2020-10-14"
```

- Set the backtesting to date to first of December 2021:
```
engine -to "2021-12-01"
```

- Set the stoploss to -50:
```
engine -sl -50
```

- Set the stoploss type to trailing:
```
engine -sl_type "trailing"
```

- Turn off the plotting functionality:
```
engine -no-plots True
```

- Turn on the hyperoptimization functionality:
```
engine -hy True
```

- Set the number of trials for the hyperoptimization functionality:
```
engine -hy True -nt 50
```

- Export the backtesting results to a json file:
```
engine -ex True
```

- Run the Engine without Engine Use Statistics:
```
engine -nostat True
```

The Engine Use Statistics pertains to the statistics we collect about the Engine usage. We only collect completely
anonymised user ID's, current Engine version, and when the Engine was run.