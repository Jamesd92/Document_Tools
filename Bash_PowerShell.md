# Bash and PowerShell Guide

## Overview

This document covers how to use PowerShell and Bash, it is explains to users some helpful commands and how to quickly navigate the file system. Due to most work environment being windows based operating system their will be preamble on the software that needs to be installed for bash and other supporting applications. The intent is to move all commands to powershell utilizing app-get, scoop and win-get, however some applications my need to be manually downloaded.

## Preamble

To utilise bash on windows operating system the bash the user must download bash from their website [git-bash](https://git-scm.com/downloads), once it is downloaded an installed bash cn be utilised.

PowerShell works straight out of the box for windows however it is recommended to use PowerShell 7 from with windows store. Other useful applications from the windows store include the windows terminal, this will allows multiple shells to be open in the one terminal.

## Windows Terminal

Windows terminal allows multiple shells to be opened in the one terminal and expedites how fast an operator can navigate when utilising multiple BASH/PowerShell/Cmd Termainals or utilising the WSL (windows Subsystem for Linux) shell. Windows Terminal can be downloaded from the windows shop with two versions available Windows Terminal and Windows Terminal (Preview). The preview version is the non-stable version with the up and coming features, my recommendation is to use the Preview version as its' current features have improved users attributes.

This section covers the below points to assist the using in setting up Windows Terminal and Operating Windows Terminal.

1. Key Binds
2. Json file
3. Adding Shells

### Short Cuts

The below table defines commonly used short cuts which will help when using Windows Terminal

| Description                              | Key Bind             |
| ---------------------------------------- | -------------------- |
| Open a new Windows Terminal instance     | Ctrl + Shift + N     |
| Open a new default profile tab           | Ctrl + shift + T     |
| Switch to the Next tab                   | Ctrl + Tab           |
| Open the profile selection dropdown Menu | Ctrl + Shift + Space |
| Open another instance of the current tab | Ctrl + Shift + D     |
| Close the current tab                    | Ctrl + W             |
| Close other tabs                         | Ctrl + Shift + W     |
| Create/Split a Vertical Pane             | Alt + Shift + '+'    |
| Create/Split a Horizontal pane           | Alt + Shift + '-'    |
| Resize the current Pane Up               | Alt + Shift + ↑      |
| Resize the current Pane Down             | Alt + Shift + ↓      |
| Resize the current Pane Left             | Alt + Shift + ←      |
| Resize the current Pane Right            | Alt + Shift + →      |
| Increase the font size                   | Ctrl + =             |
| Decrease the font size                   | Ctrl + '-'           |
| Reset the font size to the default       | Ctrl + 0             |
| Scroll up in the Windows Terminal        | Ctrl + Shift ↑       |
| Scroll down in the windows Terminal      | Ctrl + Shift ↓       |
| Move focus to one pane up                | alt + ↑              |
| Move focus to one pane down              | alt + ↓              |
| Move focus to one pane left              | alt + ←              |
| Move focus to one pane right             | alt + →              |

### Json File

Windows Terminal can be configured either through the GUI through the key bind (Ctrl + ,) or through the settings in the top ribbon. For users which do not wish to have a replicatable work environment they can configure how each shell looks through the GUI. I would however recommend utilising the json file, as this can be used to load your terminal setting on other machines by simply copying the JSON from your existing computer to your new one.

The file is broken into section the below sections.

Keybind: This section defines the keybinds and operators have the capacity to change them as they desire the syntax for the keybinds are defined below.

<!-- prettier-ignore-start -->
[
    {
        "Command":
            {
            "action": "`keyword (closetab)`"
            },
        "keys":"`key bind (Ctrl + W)`"
    }
]

Terminal configuration: This section defines a few minor settings. The full list of options can be found at [Windows Terminal docs: Interaction](https://docs.microsoft.com/en-us/windows/terminal/customize-settings/interaction)

"CopyFormatting": "none", (true, false, all, none, html, rtf) 
"trimBlockSelection": "true", (true,false)
"trimPaste": "true", (true,false)
"defaultProfile":"{guid}", //This value determines the default shell that will be launched when a new shell is required, the guid links to the guid's in each list.
"profiles":

{
  "defaults": {
    // Any settings here apply to all profiles 
  },

The List section defines which shells are accessible through the terminal their many switches or configuration values that can be added for a shells launch, for more information view [Microsoft Profile - General](https://docs.microsoft.com/en-us/windows/terminal/customize-settings/profile-general)
  "list":
  [
    {
      "backgroundImage": "C:\\Users\\james.don\\.JamesConfig\\PowerShell.png", //Image to use
      "backgroundImageAlignment": "bottomRight", //Image location 
      "backgroundImageStretchMode": "none", 
      "colorScheme": "Campbell Powershell", //Colour used
      "commandline": "%SystemRoot%\\System32\\WindowsPowerShell\\v1.0\\powershell.exe", //Calls the shell to open.
      "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}", //The unique identifier.
      "hidden": false, //Defines if the tab is shown in the drop down list.
      "name": "Windows PowerShell"  //This defines what the tab will be called. 
    }
  ]
}
<!-- prettier-ignore-end -->
