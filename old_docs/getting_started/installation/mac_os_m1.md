# Getting started on MacOS (M1 Chip)

## Apple Silicon M1 Chip
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

### Continue by reading [Running with Python](https://docs.dematrading.ai/getting_started/running/running_python)