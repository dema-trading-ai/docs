# Getting started for Windows

## How to install on a Windows device (without Docker)
Installing the Engine on a Windows device requires the following steps:

1. Install Python 3 ([click here to download Python](https://www.python.org/downloads/))
2. Make sure pip is installed (Pip should be installed automatically on any version of Python that is 3 
   or above. If it is not installed on your system [click here](https://pip.pypa.io/en/stable/installing/))

3. Find your current operating system. This can be found in system settings (either 32-bit or 64-bit). Go to [this](https://www.lfd.uci.edu/~gohlke/pythonlibs/#ta-lib) link and search the page for "ta-lib".
    
    * If you have a 64-bit operating system download: `TA_Lib‑0.4.20‑cp38‑cp38‑win_amd64.whl`
    * If you have a 32-bit operating system download: `TA_Lib‑0.4.20‑cp38‑cp38‑win32.whl`

4. Open a terminal (e.g. Windows Powershell) and change to the downloads folder:
`cd [PATH/TO/DOWNLOADS/FOLDER]`

5. Install the TA-Lib wheel by running this command:
`pip install [TA_Lib-wheel].whl`

6. Clone the [Engine github repository](https://github.com/dema-trading-ai/engine) on your computer.

    
### Continue by reading [Running with Python](https://docs.dematrading.ai/getting_started/running/running_python)