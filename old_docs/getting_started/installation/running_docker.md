# Quickstart using Docker
!!! attention
    This guide assumes that docker and docker-compose are already installed on your system. ([click here to download Docker](https://docs.docker.com/get-docker/))


## Installing
The following commands will initialise the file structure used by the Engine. Run the commands in your terminal. You only need to do this once!
```
docker run -t --rm -v "$(pwd):/usr/src/engine/output" dematrading/engine:stable init <YOUR_DIRECTORY_NAME>
```
The above snippet creates a new directory containing a config file, a strategy file and a backtesting folder. Those will be used when running the Engine.
Note that you need to fill in the placeholder `<YOUR_DIRECTORY_NAME>`.


## Backtesting
Once the above is done, you're ready to start the first backtest. This can be done by running the command below.
```
# Run your first backtest
docker-compose run --rm dema-engine
```
By default, the backtest will run the sample strategy provided. This is just a reference to get you started. Don't expect
it to be profitable already, as you should adjust it to your own strategy!


## Updating the Engine with docker-compose
Updating is done by running the following command:
```
# Update the engine
docker-compose pull
```
The above command will pull the newest version of the Engine for you. That's all there is to it! The next time you run a backtest, the newest version will be used. 


## Whats next?
You are now ready to start developing your own strategies! Get started by reading [examples of strategies](https://docs.dematrading.ai/getting_started/strategies/strategyexamples/). Or have a look at [configuring backtesting](https://docs.dematrading.ai/getting_started/installation/configuring_backtest/)