# Installing Docker
***
The existing docker compose file has been improved, allowing you to use `docker-compose up` to execute and run the main program with the volume mounted. This in itself should make using Docker more user-friendly, compared to using the original `docker ...` command.

There are 2 ways of using docker-compose:
- `docker-compose up`: used to start up the containers and keeping them up.
- `docker-compose run`: used to run a one-off command, ideal and suitable for running backtests.
   
Despite this, the command to use run is only a little bit more complicated, as can be seen in the following example:

Using up:

`docker-compose up`

Using run:

`docker-compose run --rm dema-engine main.py`

Using run will stop the containers when the process is finished, whereas up will keep the container up when it's done and have to be manually exited with a simple control + C keybind.

Following the example, there's pros and cons for both commands in terms of user-friendly-ness, and functionality.
***
## Installing on MacOS
***
## Installing on Windows
***
## Installing on Linux