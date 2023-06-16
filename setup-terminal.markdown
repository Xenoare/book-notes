## Setup Terminal Windows

Ref. on [Here](https://www.youtube.com/watch?v=VT2L1SXFq9U) by Scoot Hanselman [Github](https://github.com/shanselman)

### **Get a Terminal and a Powershell**
You can install a brand new [Terminal](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701?hl=id-id&gl=id&rtc=1*) and [Powershell](https://apps.microsoft.com/store/detail/powershell/9MZ1SNWT0N5D), you also can use WSL (Windows Subsystem for Linux) to use any Linux distribution on your windows (the default itself is Ubuntu). Here's the commmand
```
wsl --install
```
* You can customize each profiles by modifying the json file

### **Adding Oh-my-posh into your shell**
Oh My Posh is a custom prompt engine for any shell. This is the installation process step-by-step
```
winget install JanDeDobbeleer.OhMyPosh -s winget
```
1. First we need to install Fonts, since Oh My Posh was designed to use (Nerd Font)[https://www.nerdfonts.com/] to include *icons* and configure to your termminal / editor (Vscode)
2. Configure your shell, first edit the powershell profile script 
```
notepad $PROFILE
```
There may be an error since we didn't create this file. Use `echo $PROFILE` to know where the profile script located. After that put this code into file.
```
oh-my-posh --init --shell pwsh --config ~/jandedobbeleer.omp.json | Invoke-Expression
```
![Oh-my-posh](https://hanselmanblogcontent.azureedge.net/Windows-Live-Writer/Creating-the-Ultimate-PowerShell-prompt_11CD9/image_c2be46cf-5d40-4ed3-8af8-63f8789456de.png)
Oh-my-posh also have .json themes directory (usually located at `oh-my-posh/themes` or just use `dir oh-my-posh.exe` to know its location)
3. You always want to make your themes, then go to [Oh My Posh Themes](https://github.com/JanDeDobbeleer/oh-my-posh/tree/main/themes?WT.mc_id=-blog-scottha) and modify your themes with your additional *segments*.

### **Turn Your Powershell directories**
![PSGallery](https://hanselmanblogcontent.azureedge.net/Windows-Live-Writer/Creating-the-Ultimate-PowerShell-prompt_11CD9/image_9a01061f-23d8-4ca9-8ee9-2b28d358ddd7.png)
If u want to have some *icons* within your directories, then first thing first is to install a module in your terminal
```
Install-Module -Name Terminal-Icons -Repository PSGallery
```
then put this line in `$PROFILE` script
```
Import-Module -Name Terminal-Icons
```

### **Add predictive autocomplete**
![PSReadLine](https://hanselmanblogcontent.azureedge.net/psreadlinehistory.gif)
History and autopredective mode is very useful. PSReadLine provide a module that can be done for this. First thing first install this
```
Install-Module PSReadLine -AllowPrerelease -Force
```
and this
```
Install-Module z -AllowClobber
```
and paste this [powershell](https://gist.github.com/shanselman/25f5550ad186189e0e68916c6d7f44c3?WT.mc_id=-blog-scottha) profile to `$PROFILE` script.

There you have it, you can still play with the segment profiles or color of the terminal itsef, there are still many ways to customize it. Have fun :)
