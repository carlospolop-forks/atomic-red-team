
# Data Obfuscation

MITRE ATT&CK Technique: [T1001](https://attack.mitre.org/wiki/Technique/T1001)



## Metasploit - Mimic Google Certificat

    use auxiliary/gather/impersonate_ssl
    set rhost www.google.com
    run

## PowerShell

    echo Get-Process | clip
    Get-Clipboard | iex
