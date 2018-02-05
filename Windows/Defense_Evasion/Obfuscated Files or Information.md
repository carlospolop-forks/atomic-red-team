
# Obfuscated Files Or Information

MITRE ATT&CK Technique: [T1027](https://attack.mitre.org/wiki/Technique/T1027)

## PowerShell Encode Command #1

    $command = 'dir –rec "c:\program files"’
    $bytes = [System.Text.Encoding]::Unicode.GetBytes($command)
    $encodedCommand = [Convert]::ToBase64String($bytes)
    echo ”powershell.exe –e $encodedCommand”

## PowerShell Encode Command #2

    ”powershell –e ”+(cmd /c echo {start-process calc.exe}).split('')[1]
