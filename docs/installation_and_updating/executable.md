# Install Engine via executable

## Installation & updating
***
### Mac
From a terminal, execute the following command: 
```
curl -fsSL https://engine-store.ams3.digitaloceanspaces.com/installing_macos.sh | /bin/bash
```
![type:video](https://www.youtube.com/embed/-C-SHgOj5Ro)

### Windows
From a Powershell window opened as **Administrator**, execute the following command:
```
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://ams3.digitaloceanspaces.com/engine-store/install-windows.ps1'))
```
![type:video](https://www.youtube.com/embed/rKLvhZVG3Po)


## Running
***
Execute the following commands from a terminal(MacOS) or Powershell(Windows)

### Creating a project
```
engine init <YOUR_DIRECTORY_NAME>
```

### Running engine
From an `engine` project directory, execute:
```
engine
```