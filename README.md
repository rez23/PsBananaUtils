# PsBananaUtils a powershell utils module
## What is this
This is a simple umbrella module that gathers together various utility modules I’ve written for myself over the years, which are very useful for many tasks in PowerShell (at least on Windows).
- [PsBananaUtils.HyperV](https://github.com/rez23/PsBananaUtils.HyperV)
- [PsBananaUtils.Miscellaunus](https://github.com/rez23/PsBananaUtils.Miscellaunus)
- [PsBananaUtils.PowerShell](https://github.com/rez23/PsBananaUtils.PowerShell)
- [PsBananaUtils.Windows](https://github.com/rez23/PsBananaUtils.Windows)
- [PsBananaUtils.WSL](https://github.com/rez23/PsBananaUtils.WSL)

## Install the module
Install the module using `Install-PsResource` or `Install-Module`:
```powershell
Install-PsResource -Name PsBananaUtils -Scope CurrentUser -TrustRepository
```
Now, you can use the applets, for example `Invoke-CustomPowershell`:
```powershell
# ls will be launch on a PowerShell env from Windows Powershell (5.1)
Invoke-CustomPowerShelln -PowerShellVersion 7 -Command {ls} | Where-Object {$_.BaseName -match ".ps1"}
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

# Import only Miscellaunus utilities
Import-Module PsBananaUtils.Miscellaunus

# Import only PowerShell utilities
Import-Module PsBananaUtils.PowerShell

# Import only Windows utilities
Import-Module PsBananaUtils.Windows

# Import only WSL utilities
Import-Module PsBananaUtils.WSL
```
## About the project
I created this module to keep together the various solutions I’ve built over time to handle tasks I often need during my daily PowerShell usage. I plan to continue adding utilities as I create them.

## Substain the project
If you like my work, leave a star on this repository or donate me a coffee:
- [PayPall.me](https://paypal.me/rez23774)
- [Ko-Fi](https://ko-fi.com/spartacoamadei)