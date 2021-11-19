# Oracle® VM VirtualBox und Windows 11 - WSL2
VBox Problemumgehungen - Arbeiten auf der Kommandozeile / Windows cmd  
* Mein Rechner hat sein Update auf Windows 11 erhalten. Dann habe ich zwei Tage WSL1, WSL2 und WSLg getestet. Noch nicht perfekt, aber brauchbar :-)  
* Dann wollte ich meine virtuellen Maschinen über Oracle VirtualBox wieder starten ... aber VBox funktionierte nicht mehr. Auch ein Update auf VBox 6.1.28 brachte nichts.  
* Deswegen musste ich auf die Windows Kommandozeile ausweichen, um meine virtuellen Maschinen starten zu können.  
**Damit ich die Befehle nicht wieder vergesse, hier das User Manual für VirtualBox 6.1: https://docs.oracle.com/en/virtualization/virtualbox/6.1/user/index.html**

```
Der Pfad zu VirtualBox auf meiner Microsoft Windows 11 Maschine:  
C:\Program Files\Oracle\VirtualBox>
also zuerst:  
cd Program Files\Oracle\VirtualBox>
```

### Anzeigen der vorhandenen Maschinen
`VBoxManage.exe list vms`  
Listet alle virtuellen Maschinen auf, die derzeit bei Oracle VM VirtualBox registriert sind. Standardmäßig wird hier eine kompakte Liste mit dem Namen und der UUID jeder VM angezeigt.

### Details zu einer VM anzeigen
`VBoxManage.exe showvminfo u20Gnome`  
Zeigt z.B. alle Details zur VM mit dem Namen "u20Gnome" an.  

### Snapshots einer VM anzeigen
`VBoxManage.exe snapshot u20Gnome list`  
Zeigt die vorhandenen Sicherungspunkte der VM "u20Gnome" an.

### VM starten
`VBoxManage.exe startvm u20Gnome`  
Startet die VM u20Gnome.  
*Mein Problem ist, das ich diese VM bei der letzten Nutzung nicht ausgeschaltet bzw. heruntergefahren, sondern nur angehalten habe. Duch das Update auf Windows 11, das herumspielen mit WSL2 und WSLg und das Update von VirtualBox von 6.1.26 auf 6.1.28 startet meine VM nicht mehr. Ich bekomme folgende Fehlermeldung:*  
``` 
Waiting for VM "u20GUI" to power on...  
VBoxManage.exe: error: apic#0: Config mismatch - uApicMode: saved=3 config=2 [ver=5 pass=final] (VERR_SSM_LOAD_CONFIG_MISMATCH)  
VBoxManage.exe: error: Details: code E_FAIL (0x80004005), component ConsoleWrap, interface IConsole  
```

### eine neue Maschine aus einem vorhandenen Snapshot clonen
`VBoxManage.exe clonevm u20Gnome --name="u20GUI" --register --snapshot="Sicherungspunkt 2"`  
Erstellt einen Clone vom "Sicherungspunkt 2" der vorhandenen VM "u20Gnome" mit dem neuen Namen "u20GUI".  
