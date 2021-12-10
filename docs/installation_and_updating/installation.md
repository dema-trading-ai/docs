---
hide:
  - toc
---

# Installation
If you want to install the Engine, all you have to do is to run a single command in your terminal. Based on which
operating system you are using, you follow the instructions below. For MacOS follow the instructions below. If you are
using Windows? Take a look at the instructions in the Windows section.

## MacOS
If your operating system is macOS, please execute the following command from a terminal: 
```
curl -fsSL https://engine-store.ams3.digitaloceanspaces.com/installing_macos.sh | /bin/bash
```
This command downloads and runs the script that installs the Engine. If you want to know the details, read through
the [installation script](https://engine-store.ams3.digitaloceanspaces.com/installing_macos.sh){target=_blank}.

For more detailed instructions, please see the video below!

![type:video](https://www.youtube.com/embed/-C-SHgOj5Ro)

## Windows
If your operating system is Windows, the command you have to run is different. To install the Engine, open a Powershell
window as Administrator. Then, execute the following command:
```
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://ams3.digitaloceanspaces.com/engine-store/install-windows.ps1'))
```
This command downloads and runs the script that installs the Engine. If you want to know the details, read through
the [installation script](https://ams3.digitaloceanspaces.com/engine-store/install-windows.ps1){target=_blank}.

For more detailed instructions, please see the video below!

![type:video](https://www.youtube.com/embed/rKLvhZVG3Po)

