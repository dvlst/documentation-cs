## Reverse Shell
- [Reverse Shell Cheat Sheet](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md)

## Add VMware share in Kali
1. Add share over VMware GUI
2. In Kali Linux edit /etc/fstab
```
.host:/  /mnt/hgfs/  fuse.vmhgfs-fuse  defaults,allow_other,uid=1000  0  0
```
3. Create folder and connect with VMware share
```
sudo mkdir -p /mnt/hgfs/
```

```
sudo /usr/bin/vmhgfs-fuse .host:/ /mnt/hgfs/ -o subtype=vmhgfs-fuse,allow_other
```

## [CyberChef](https://gchq.github.io/CyberChef/)
- Tool zum encoden von gängigen Verschlüsselungsmethoden

## grep
- Filtern von Logs
- [Syntax](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)

## [json2csv](https://www.npmjs.com/package/json2csv)
- Tool zum konvertieren von JSON zu CSV
- Benötigt [NodeJS](https://nodejs.org/en/)

### Syntax
- Installation
```
sudo npm install -g json2csv 
```

- Aus JSON File CSV generieren
```
json2csv -i [JSON-Pfad] -o [CSV-Pfad]
```

### Alternative MacOS
- Excel > Data > Get Data > From Text > UTF-8 > Delimiter definieren

## [Amnesia](https://github.com/dTsitsigkos/Amnesia)
- Anonymization Tool
- [Alternative](https://arx.deidentifier.org/downloads/)

## [hashcat](https://hashcat.net/hashcat/)
- Password Cracker Tool
- Benötigt eine Liste mit Passwörten
	- Beispielsweise [rockyou.txt](https://github.com/ohmybahgosh/RockYou2021.txt)
```
hashcat -m 0 --show hash-file rockyou.txt
```

## PID an Prozess zuordnen
- PID Prozess zuordnen (Windows)
```
tasklist | find [PID]
```

- PID Prozess zuordnen (Linux)
```
ps -ef | grep [PID]
```