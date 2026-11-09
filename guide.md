# Bash Setup Guide on Windows
So you want to run and write Bash Scripts on Windows, but a Virtual Machine (VM) is too much for you? Well you know what, there's a solution for you, and it's called WSL (or Windows Subsystem for Linux)!

## Huh, what's WSL?

Happy that you're asking! WSL, also known as Windows Subsystem for Linux, is a Windows feature that lets you run a Linux environment on your Windows machine, without the need of a heavy virtual machine or dual booting. It lets you run Linux commands (including Bash scripts!), GUI apps (Windows 11 or 10 Build 19044 or newer), etc. 

WSL runs inside of a Hyper-V virtual machine. There's two version of WSL, WSL1 and WSL2. This guide will assume you are using the latest WSL2. You can read [here](https://learn.microsoft.com/en-us/windows/wsl/compare-versions) the difference between the two, and you can use:
```powershell
wsl --set-version <distro-name> 2
```
to upgrade a specific WSL distro to WSL2. 

## I'm interested, what are the prerequisites?

You need to have either Windows 11 or Windows 10 version 2004 and higher (Build 19041 and higher). You can verify that by pressing `Windows+R`, then typing `winver`, then enter. You'll see the build number in the window that opens up, like here:  
![winver window](assets/winver.png)  
You don't even need it to be an activated copy of Windows! 
Both ARM64 and x64 (Intel/AMD) CPUs are supported. If you're running Windows in a VM (in which case, honestly, why are you bothering to install WSL?), you must make sure that nested virtualization is enabled.

This guide will assume you are running one of the supported Windows version. If you aren't, you can still install WSL manually by following [this Microsoft guide](https://learn.microsoft.com/en-us/windows/wsl/install-manual).

## Okay, how do we install this?
I'll guide you through this!

### Step 1: Checking whether WSL is already installed
First, open a Windows CMD window as Administrator:
![Open CMD as Administrator](assets/cmd-admin.png)

In the command prompt that opens up, type the following command to verify if WSL isn't installed already:
```
wsl.exe --list --verbose
```
If you get a message like the one in the screenshot below, that means that WSL isn't yet installed on your system, so you can safely press `CTRL+C`. 
![WSL is not installed](assets/WSL-not-installed.png)

If you obtain a different message, like the one below, then that means that WSL is already installed. You can skip to step 3.

If you see a table with a distribution you want to use

### Step 2: Installing WSL itself

Now we can install the WSL feature itself. Usually you install WSL with the default provided Linux distribution (usually Ubuntu), but here I'll show you how to install it with no distribution so we can choose the one we will want to work with in the next step.

Still in your Administrator command prompt, type:
```
wsl --install --no-distribution
```
It will install the required components, so this may take a while. If everything goes well, the command should output:
>The requested operation is successful. Changes will not be effective until the system is rebooted.  

You can now reboot!

### Step 3: Choosing a distribution

Now that you have rebooted, check that everything works fine by opening an Administrator CMD and running again:
```
wsl --list --verbose
```
You should get a message telling you that no distribution is currently installed, like shown below:
![WSL installed but showing no distributions](assets/WSL-installed-no-distro.png)

As the message suggests, we can run:
```
wsl --list --online
```
to list distributions that are available for download. It gives quite a long list:
![distro list](assets/distro-list.png)

I won't cover what each distribution is, but here's a quick breakdown of the important ones (if you don't know which to pick, a safe choice would be Ubuntu):

- Debian: a pretty stable and relatively user-friendly distribution, uses the _apt_ package manager.
- Ubuntu: based on Debian, more user-friendly, also uses the _apt_ package manager.
- Kali Linux: a hacking distribution based on Debian. Not really useful if you don't need the hacking tools included in it. Also uses the _apt_ package manager.
- Arch Linux: a bleeding-edge distribution, less user-friendly than Debian-based distributions, but gets you the latest software by default. Uses the _pacman_ package manager.
- Fedora: a bleeding-edge distribution, although more stable than Arch. Uses the _DNF_ package manager.

For this guide we will stay with something simple (as we really don't need anything more than running Bash scripts) and we will take Ubuntu. If you prefer to use another distribution, that's your call, just make sure to use the correct package manager command when needed, as for the rest of this guide we will assume that you are using _apt_.

When you're ready, you can run:
```
wsl --install <distribution name>
```
to install your chosen distro. Here I'm installing Ubuntu:
![Ubuntu installing](assets/ubuntu-install.png)
(You may get, like me, a message saying that nested virtualization isn't available. For some reasons it appears but if the installation continues then you're fine).  
When this is done you'll get a prompt saying `Create a default Unix user account:`. Type the username that you wish to use inside of this WSL instance, then press `Enter`, then choose a password and confirm it.

Opt out of the analytics by typing `n` then `Enter` and... we're in!  
![Ubuntu prompt](assets/ubuntu-prompt.png)

#### Updating

Now that we're inside of the system, the first thing we should do is updating. On Ubuntu (or any Debian-based systems), you can do so by running:
```bash
sudo apt update
sudo apt upgrade
```
This may take a while, so be patient!.