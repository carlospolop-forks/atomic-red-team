## Permission Groups Discovery

MITRE ATT&CK Technique: [T1069](https://attack.mitre.org/wiki/Technique/T1069)

## Old way with net – does not support recursive searches

    CMD> net group “domain admins” /domain

#Recursively searching active directory groups
    
    PS> Get-NetGroupMember 'Domain Admins' -Recurse | Select MemberName

#From a file with multiple groups using the pipeline

    PS> Get-Content groups.txt | Get-NetGroupMember -Recurse | Select MemberName

#Check for users who don't have kerberos preauthentication set

    PS> Get-DomainUser -PreauthNotRequired
    PS> Get-DomainUser -UACFilter DONT_REQ_PREAUTH

#Find all service accounts in "Domain Admins"

    PS> Get-DomainUser -SPN | ?{$_.memberof -match 'Domain Admins'}

#Use an alternate creadential for any function

    PS> $SecPassword = ConvertTo-SecureString 'BurgerBurgerBurger!' -AsPlainText -Force
    PS> $Cred = New-Object System.Management.Automation.PSCredential('TESTLAB\dfm.a', $SecPassword)
    PS> Get-DomainUser -Credential $Cred
