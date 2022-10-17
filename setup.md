# WSL Installation Guide

By James Don
Date 17/10/2022

This document will cover how to install WSL 2 with an ubuntu distribution. This guide is based of [Microsofts guide](https://learn.microsoft.com/en-us/windows/wsl/install) for more information
please refer to their guide.

## Important notes

Ensure your windows version is above Windows 10 2004 and Higher Build version of 19041 or higher. Currently all windows 11 builds work.

The WSL image has to be a WSL 2 image and not a WSL 1 image, this is important when installing the WSL images.

The main reason for this guide is for the purpose to run **DOCKER**. If you install Docker and VMware they will both for the Hyper-V communications protocol which will cause both applications not work.
To run both DOCKER and a WSL 2 installation in required, this is because WSL 2 runs a GNU Kernel which allows a linux Distribution to run and DOCKER to mount to.

## Overview

To install WSL and Docker please follow the below steps.

1. Install WSL
2. Installing Ubuntu
3. Upgrade WSL Version 1 to Version 2
4. Install DOCKER for windows

## Installing WSL

To install WSL it is recommend (my experience) to install it by going through the GUI however below I have listed how to install it through the command line.

### GUI

Start -> "Turn Windows features on or off" -> Turn on "Windows Subsystem for linux"

After you have selected and installed the Windows Subsystem for Linux application you will need to restart you system.

Then set WSLs default version to 2. Open Powershell and Run the below code.\
`wsl --set-default-version 2`

### Command Line

To install WSL from the command line run the below commands in powershell (administrator)

`wsl --install`\
`wsl --set-default-version 2`

If you have any issues you may need to run the below commands

dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart \
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart \
Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform -NoRestart

## Installing Ubuntu

Confirm that WSL installed correctly by typing the below command.

`wsl -l -v`

A list of distributions should appear, as seen below.
`Ubuntu Ubuntu`\
`Debian Debian GNU/Linux`\
`kali-linux Kali Linux Rolling`\
`openSUSE-42 openSUSE Leap 42`\
`SLES-12 SUSE Linux Enterprise Server v12`\
`Ubuntu-16.04 Ubuntu 16.04 LTS`\
`Ubuntu-18.04 Ubuntu 18.04 LTS`\
`Ubuntu-20.04 Ubuntu 20.04 LTS`

If the above list or similar does not appear your WSL may have installed incorrectly.

Choose any of the Distributions listed in the `wsl -l -v` I would recommend Ubuntu-20.04 however any Ubuntu-xx.xx will work.

`wsl --install -d Distributions-Name`\
`wsl --install -d Ubuntu-20.04 `

The distribution will then install and be ready for DOCKER to be installed. It can be noted that DOCKER can be installed prior to having a WSL distribution installed.

As a final check it is recommend to run the below command to confirm that the distribution is as WSL 2 image, if the version returns 1 instead of 2 please continue to the
section, upgrading a WSL 1 image to WSL 2.

`wsl -l -v`

Output:
`NAME STATE Version`\
`Ubuntu-20.04 Stopped 2`

## Updating a image from WSL 1 to WSL 2

If you have built a WSL 1 image by accident no issue it is a simple task to update from WSL 1 to WSL 2.

First confirm the distribution version by running the below script.

`wsl -l -v`

Then on the WSL distribution run

`wsl --set-version <Distribution> 2`\
`wsl --set-version ubuntu-20.04 2`

## Installing Docker

To install docker navigate to the DOCKER for windows installation [here](https://docs.docker.com/desktop/install/windows-install/) and install the client. Ensure that the tick box `USE WSL2` is selected during the installation configuration.
