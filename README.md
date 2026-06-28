# 🍌 PsBananaUtils a collection of helpers for Windows PowerShell
## What is this
This is a simple umbrella module that gathers together various utility modules I’ve written for myself over the years, which are very useful for many tasks in PowerShell (at least on Windows).  

- [PsBananaUtils.HyperV](https://github.com/rez23/PsBananaUtils.HyperV)
- [PsBananaUtils.Miscellaneous](https://github.com/rez23/PsBananaUtils.Miscellaneous)
- [PsBananaUtils.PowerShell](https://github.com/rez23/PsBananaUtils.PowerShell)
- [PsBananaUtils.Windows](https://github.com/rez23/PsBananaUtils.Windows)
- [PsBananaUtils.WSL](https://github.com/rez23/PsBananaUtils.WSL)

## Install the module
Install the module using `Install-PsResource` or `Install-Module`:
```powershell
Install-PsResource -Name PsBananaUtils -Scope CurrentUser -TrustRepository
```
Now, you can use the cmdlets, for example `Invoke-CustomPowerShell`:
```powershell
# ls will be launched in a PowerShell 7 environment from Windows PowerShell (5.1)
Invoke-CustomPowerShell -PowerShellVersion 7 -Command {ls} | Where-Object {$_.BaseName -match ".ps1"}
```
or `Get-NetAdaptersInfo`
```powershell
Get-NetAdaptersInfo | Where-Object {$_.Name -match "ethernet"}
```
## Import the module
If you need to import the modules you can import the main `PsBananaUtils` module:
```powershell
Import-Module PsBananaUtils
```
or import individual submodules:
```powershell
# Import only HyperV utilities
Import-Module PsBananaUtils.HyperV

# Import only Miscellaneous utilities
Import-Module PsBananaUtils.Miscellaneous

# Import only PowerShell utilities
Import-Module PsBananaUtils.PowerShell

# Import only Windows utilities
Import-Module PsBananaUtils.Windows

# Import only WSL utilities
Import-Module PsBananaUtils.WSL
```
## More info about
This is only an umbrella module that "contains" all the PsBananaUtils functionalities.  
Anyway, you aren't forced to install the whole package if you don't want to. Instead, you can install only the features that you need and want.  
```powershell
# Install only HyperV features subset from PsBananaUtils
Install-PsResource -Name PsBananaUtils.HyperV

# Install only WSL features subset from PsBananaUtils
Install-PsResource -Name PsBananaUtils.WSL

# Install only Windows features subset from PsBananaUtils
Install-PsResource -Name PsBananaUtils.Windows

# Install only PowerShell features subset from PsBananaUtils
Install-PsResource -Name PsBananaUtils.PowerShell

# Install only Miscellaneous features subset from PsBananaUtils
Install-PsResource -Name PsBananaUtils.Miscellaneous
```
## Modules overviews
`PsBananaUtils` does not export anything itself; it is more or less a namespace package for the child modules described above. Here I provide a brief explanation of what each module is:
- `PsBananaUtils.HyperV`: The main goal is to manage your Hyper-V VMs by saving a default VM setup (credentials and VM name).
- `PsBananaUtils.Windows`: Basically provides some aliases and helper functions for Windows, like creating junctions and checking adapters and IPs.
- `PsBananaUtils.WSL`: Not much here for now, mainly provides `Optimize-WslVirtualDrive`, which allows shrinking WSL VHDs to reclaim disk space.
- `PsBananaUtils.PowerShell`: Includes many handlers and utility functions that enhance everyday PowerShell usage.
- `PsBananaUtils.Miscellaneous`: Mainly provides `Get-SingleFolderFromGitRemote`

Use Get-Help and Get-Command to have more info about the module
```
Get-Command -Module PsBananaUtils*
Get-Help Get-VirtualMachineInfo
```
## About the project
I created this module to keep together the various solutions I’ve built over time to handle tasks I often need during my daily PowerShell usage. I plan to continue adding utilities as I create them.

## Some usefull things in this module:
- `Invoke-CustomPowerShell`:<br>
This command permit to launch a command inside a custom powershell version on the local machine maintaining PowerShell object serialization:
```powershell
Invoke-CustomPowerShell -Version 7 -Command {ls} | ? { 
    # This work becouse serialization is rebuilt from 
    # custom pwsh.exe output
    $_.BaseName -match ".ps1" 
}
```
- `Invoke-CustomPowerShell` from [`PsBananaUtils.PoerShell`](https://github.com/rez23/PsBananaUtils.PowerShell):<br>
permit also to launch custom PowerShell binary of your choice
```powershell
Invoke-CustomPowerShell -CustomPowerShellPath "C:\pwsh.exe" -Command {ls}
```
There is also a command to check what PowerShell version are on current machine
```powershell
Get-PowerShellVersions -All
```
- the`*-VirtualMachine*` commands from [`PsBananaUtils.HyperV`](https://github.com/rez23/PsBananaUtils.HyperV):<br>    
Permit to "register" a preferred HyperV session for VMName and Credential
```powershell
Register-VirtualMachineAliasesConfig -Credential (Import-Clixmap -Path "C:\MyCert.xml") -VMName "My VM"
# from now you can launch Vm command directly in this session
Invoke-VirtualMachine -Command {ls}
```
- `Get-VirtualMachineInfo` from [`PsBananaUtils.HyperV`](https://github.com/rez23/PsBananaUtils.HyperV):<br>
Return info (with available IP addresses) from Registered VM config or against all your VMs
```powershell
# Get Ipv4 addresses of all available VM
Get-VirtualMachineInfo -All | % {$_.IPv4}
```
- `Get-NetAdaptersInfo` from [`PsBananaUtils.Windows`](https://github.com/rez23/PsBananaUtils.Windows):<br>
Return all Network adapters on current machine with its Ip addresses
```powershell
# Get all ethernet adapters and its associated Ip from machine
Get-NetAdapatersInfo | ? {$_Name -match "ethernet"}
```
- `New-*` aliases from [`PsBananaUtils.Windows`](https://github.com/rez23/PsBananaUtils.Windows):<br>
Simple provide some aliases functions to `New-Item -ItemType Directory` eccetera that maintains completion
- `Optimize-WslVirtualDrives` from [`PsBananaUtils.WSL`]:<br>
Optimize WSL and Docker VHD image to reclaim your free disk space (a well know WSL bug)
```powershell
Optimize-WslVirtualDrives
```


And more. Get all available commands using `Get-Command`:
```powershell
Get-Command -Module PsBananaUtils*
```
and if you need get more docs with `Get-Help`

[Get it on PowerShell Gallery](https://www.powershellgallery.com/packages/PsBananaUtils)

## Support the project
If you like my work, leave a star on this repository or donate me a coffee:
- [Ko-Fi](https://paypal.me/rez23774)
- [PayPal.me](https://ko-fi.com/spartacoamadei)
