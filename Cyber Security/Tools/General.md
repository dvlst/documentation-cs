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

