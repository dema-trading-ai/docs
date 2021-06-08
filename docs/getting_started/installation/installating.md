# Installing
There are multiple ways to run our Backtesting Engine. For each way, the installation steps are
outlined below. 

!!! attention Running without Docker? You will have to manually download the repository on your computer.
This can be done by [downloading the zip file](https://github.com/dema-trading-ai/engine/archive/refs/heads/main.zip)
or by [cloning the engine](https://github.com/dema-trading-ai/engine) using [Github Desktop](https://desktop.github.com)
(or something similar). 

### Utilities
The following utilities will make your life much easier during strategy development:
1. A code editor such as [Pycharm](https://www.jetbrains.com/pycharm/) or [VSCode](https://code.visualstudio.com)

### How to install with Docker (recommended)
Installing the Engine with Docker just takes a few simple steps.
[Follow the instructions here](https://docs.dematrading.ai/getting_started/installation/installing_docker).

### How to install without Docker on a macOS device (alternative)
Installing the Engine on a MAC-OS requires the following steps:

1. Install Python 3 ([click here to download Python](https://www.python.org/downloads/))
2. Install Homebrew (recommended). Installing homebrew can be done by copying the following line into your terminal app:
    
    `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
   
   OR
   
   Make sure pip is installed (alternative) (Pip should be installed automatically on any version of Python that is 2.7 
   or above. If it is not installed on your system [click here](https://pip.pypa.io/en/stable/installing/))
3. Download and install [Xcode12](https://developer.apple.com/download/)
4. Install the TA-Lib dependencies ([follow the instructions given underneath the dependencies header](https://github.com/mrjbq7/ta-lib))
5. Install TA-Lib

    By using Homebrew: (recommended)
   
    `brew install ta-lib`
    
    By using pip: (alternative)
    
    `pip install ta-lib`
   
6. Clone the [Engine github repository](https://github.com/dema-trading-ai/engine) on your computer.

### How to install without Docker on a Windows device (alternative)
Installing the Engine on a Windows device requires the following steps:

1. Install Python 3 ([click here to download Python](https://www.python.org/downloads/))
2. Make sure pip is installed (Pip should be installed automatically on any version of Python that is 2.7 
   or above. If it is not installed on your system [click here](https://pip.pypa.io/en/stable/installing/))
3. Install the TA-Lib dependencies ([follow the instructions given underneath the dependencies header](https://github.com/mrjbq7/ta-lib))
4. Install TA-Lib

    By using Homebrew: (recommended)
   
    `brew install ta-lib`
    
    By using pip: (alternative)
    
    `pip install ta-lib`
5. Clone the [Engine github repository](https://github.com/dema-trading-ai/engine) on your computer.
    

## Running the Engine
### Running with Docker

The following command will run a backtest:
```
docker-compose up
```


### Running without Docker

First run:

    `pip install -r requirements.txt`

After installing, you can run the backtesting module:

    `python3 main.py`

### Apple Silicon M1 Chip

With the new M1 Chip by Apple Silicon, there are several compatibility issues with the packages required. While Docker 
works; TA-Lib, Pandas, and even Numpy are not compatible with the chip as of yet. The M1 Chip operates with ARM rather
than x86, causing issues with regards to these Python packages. Sadly, this is not something we can fix ourselves, as this
is on the creators behind these packages and Apple itself. However, there are a few solutions that might help you to make
it work on your Apple M1 machine.

1. Open your Terminal application with Rosetta 2 and then run the script.
2. You're ready to go!

If it doesn't work with Rosetta, don't worry! There is another solution. Just follow these steps:

1. Download [Xcode12](https://developer.apple.com/download/)
2. Install [Miniforge](https://github.com/conda-forge/miniforge)
3. Create and activate a Conda environment with the following commands (don't forget to start up a new .zsh session after
having installed Miniforge)

    `conda create --name mytf`

    `conda activate mytf`
    
4. Use conda to install Python 3.8 and TA-lib in your new environment with the following commands:

    `conda install -y python==3.8.6`

    `conda install -y pandas TA-Lib`
    
5. The engine is now ready to run on your Apple M1 machine.
