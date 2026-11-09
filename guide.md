# Bash Setup Guide on Windows
So you want to run and write Bash Scripts on Windows, but a Virtual Machine (VM) is too much for you? Well you know what, there's a solution for you, and it's called WSL (or Windows Subsystem for Linux)!

## Huh, what's WSL?

Happy that you're asking! WSL, also known as Windows Subsystem for Linux, is a Windows feature that lets you run a Linux environment on your Windows machine, without the need of a heavy virtual machine or dual booting. It lets you run Linux commands (including Bash scripts!), GUI apps, etc. 

WSL runs inside of an HyperV virtual machine. There's two version of WSL, WSL1 and WSL2. This guide will assume you are using the latest WSL2. You can read [here](https://learn.microsoft.com/en-us/windows/wsl/compare-versions) the difference between the two, and you can use:
```powershell
wsl --set-version <distro-name> 2
```
to upgrade a specific WSL distro to WSL2. 

## I'm interested, what are the prerequisites?

You need to have either Windows 11 or Windows 10 version 2004 and higher (Build 19041 and higher). Both ARM x64 and Amd x64 CPUs are supported. If you're running Windows in a VM (in which case, honestly, why are you bothering to install WSL?), you must make sure that nested virtualization is enabled.

