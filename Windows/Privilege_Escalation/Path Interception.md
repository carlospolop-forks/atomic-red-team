## Path Interception

MITRE ATT&CK Technique: [T1034](https://attack.mitre.org/wiki/Technique/T1034)

[Service-Perms](https://github.com/nettitude/PoshC2/blob/master/Modules/Service-Perms.ps1)

#Service-Perms outputs a report and checks all services and folders

    PS> Import-Module Service-Perms.ps1
    PS> Get-ServicePerms

#PowerUp checks service permissions amongst other local priv esc

    [PowerUp] (https://github.com/PowerShellEmpire/PowerTools/blob/master/PowerUp/PowerUp.ps1)
    PS> Import-Module PowerUp.ps1
    PS> Invoke-AllChecks

#Manually with powershell
    
    PS> Get-WmiObject win32_service | ?{$_.Name -like '*'} | select Name, PathName -expandproperty pathname

#Manually with a GUI
    
    PS> msinfo32.exe
