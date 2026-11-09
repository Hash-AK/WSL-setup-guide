# Bash Setup Guide on Windows
So you want to run and write Bash Scripts on Windows, but a Virtual Machine (VM) is too much for you? Well you know what, there's a solution for you, and it's called WSL (or Windows Subsystem for Linux)!

## Huh, what's WSL?

Happy that you're asking! WSL, also known as Windows Subsystem for Linux, is a Windows feature that lets you run a Linux environment on your Windows machine, without the need of a heavy virtual machine or dual booting. It lets you run Linux commands (including Bash scripts!), GUI apps (Windows 11 or 10 Build 19044 or newer), etc. 

WSL runs inside of an Hyper-V virtual machine. There's two version of WSL, WSL1 and WSL2. This guide will assume you are using the latest WSL2. You can read [here](https://learn.microsoft.com/en-us/windows/wsl/compare-versions) the difference between the two, and you can use:
```powershell
wsl --set-version <distro-name> 2
```
to upgrade a specific WSL distro to WSL2. 

## I'm interested, what are the prerequisites?

You need to have either Windows 11 or Windows 10 version 2004 and higher (Build 19041 and higher). You can verify that by pressing `Windows+R`, then typing `winver`, then enter. You'll see the build number in the window that opens up, like here:  
![winver window](assets/winver.png)  
You don't even need it to be an activated copy of Windows! 
Both ARM64 and x64 (Intel/AMD) CPUs are supported. If you're running Windows in a VM (in which case, honestly, why are you bothering to install WSL?), you must make sure that nested virtualization is enabled.

This guide will assume you are running one of the supported Windows 11 version. If you aren't, you can still install WSL manually by following [this Microsoft guide](https://learn.microsoft.com/en-us/windows/wsl/install-manual).

## Okay, how do we install this?
I'll guide you through this!

### Step 1: Checking if WSL isn't already installed
First, open a Windows CMD window as Administrator:
![Open CMD as Administrator](assets/cmd-admin.png)

In the command prompt that opens up, type the following command to verify if WSL isn't installed already:
```
wsl.exe --list --verbose
```
If you get a message like the one in the screenshot below, that means that WSL isn't yet installed on your system, so you can safely press `CTRL+C`. 
![WSL is not installed](assets/WSL-not-installed.png)

If you obtain a different message, like the one below, then that means that WSL is already installed. You can skip to step 3.

### Step 2: Installing WSL itself

Now we can install the WSL feature itself. Usually you install WSL with the default provided Linux distribution (usually Ubuntu), but here I'll show you how to install it with no distribution so we can choose the one we will want to work with in the next step.

Still in your Administrator command prompt, type:
```
wsl --install --no-distribution
```
It will install the required components, so this may take a while. If everything goes well, the command should output :
>The requested operation is successful. Changes will not be effective until the system is rebooted.  

You can now reboot!

### Step 3: Choosing a distribution

Now that you have rebooted, check that everything works fine by running again:
```
wsl.exe --list --verbose
```
You should get a message telling you that no distribution is currently installed, like shown below:
![WSL installed but showing no distributions](assets/WSL-installed-no-distro.png)
