---
layout: post
title: Installing Windows Subsystem Linux (WSL2) and Docker in Windows 10
category: MLOps
---

Installing Docker in Windows system is not always a straight-forward process since Windows 10 doesn't provide support for Hyper-V. Though it provides Windows Hypervisor Platform, it doesn't help for Docker installation. We must install WSL in order to install an run Docker in our Windows system.

Run the following commands in your CMD/PowerShell with admin privilege to get the process done!

#### First check whether Hypervisor is enables in your system or not
`systeminfo`
After running the above command scroll down to the last and check the **Hyper-V Requirements** section. If its not enabled, enable it from BIOS. If it is enabled then proceed to the next command.

#### Install Microsoft Windows Subsystem Linux
`dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart`

#### Install Virtual Machine Platform
`dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart`

####  Download and Install WSL2
Use this [https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi) link to download WSL2. After downloading, install it.

#### Set WSL 2 as your default version
`wsl --set-default-version 2`

#### Install your Linux distribution of choice
Check the available linux distors by running `wsl --list --online`. Let's install Ubuntu 20.04.
`wsl --install -d Ubuntu-20.04`

####  Download and Install Docker
Download Docker from https://www.docker.com/products/docker-desktop[](https://www.docker.com/products/docker-desktop) and install t.


For latest update on WLS installation in Windows, please follow [this](https://docs.microsoft.com/en-us/windows/wsl/install-win10) official page.