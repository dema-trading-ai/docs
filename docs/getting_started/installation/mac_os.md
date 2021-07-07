# Getting started for MacOS / Linux

!!! attention "Using MacOS with M1 chip?"
    If you are running on a Mac with a M1 chip, please continue reading [here](https://docs.dematrading.ai/getting_started/installation/mac_os_m1)
    
## How to install on MacOS with Python
Installing the Engine on a MAC-OS requires the following steps:

1. Install Python 3 ([click here to download Python](https://www.python.org/downloads/))
2. Install Homebrew (recommended). Installing homebrew can be done by copying the following line into your terminal app:
    
    `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
   
   OR
   
   Make sure pip is installed (alternative) (Pip should be installed automatically on any version of Python that is 3 
   or above. If it is not installed on your system [click here](https://pip.pypa.io/en/stable/installing/))
3. Download and install [Xcode12](https://developer.apple.com/download/)
4. Install the TA-Lib dependencies ([follow the instructions given underneath the dependencies header](https://github.com/mrjbq7/ta-lib))
5. Install TA-Lib

    By using Homebrew: (recommended)
   
    `brew install ta-lib`
    
    By using pip: (alternative)
    
    `pip install ta-lib`
 
6. Clone the [Engine github repository](https://github.com/dema-trading-ai/engine) on your computer.

### Continue by reading [Running with Python](https://docs.dematrading.ai/getting_started/running/running_python)