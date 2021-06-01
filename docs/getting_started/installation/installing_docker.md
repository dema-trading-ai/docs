# Quickstart using Docker
***
!!! attention
    this guide assumes that docker and docker-compose are already installed on your system. ([click here to download Docker](https://docs.docker.com/get-docker/))


### Installing
The following commands will initialise the file structure used by the Engine. Run the commands in your terminal. You only need to do this once!
```
# Make a new directory
mkdir dema-engine
cd dema-engine

# Initialize the dema-engine workspace
docker run -v "$PWD:/usr/src/engine/output" dematrading/engine:stable init
```
The above snippet creates a new directory called 'dema-engine' and changes the working directory to the folder we just created. 
Notice how a config file, a strategy file and a backtesting folder have been created. Those will be used when running the Engine.



### Backtesting
Once this is done, you're ready to start the first backtest. This can be done by running the command below.
```
# Run your first backtest
docker-compose up
```
By default, the backtest will run the sample strategy provided. This is just a reference to get you started. Don't expect
it to be profitable already, as you should adjust it to your own strategy!


### Updating the Engine with docker-compose
Updating is done by running the following command:
```
# Update the engine
docker-compose pull
```
The above command will pull the newest version of the Engine for you. Thats all there is to it! The next time you run a backtest, the newest version will be used. 


### Whats next?
You are now ready to start developing your own strategies! Get started by reading [examples of strategies](https://docs.dematrading.ai/getting_started/strategies/strategyexamples/).