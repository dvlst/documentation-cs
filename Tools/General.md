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

### Syntax
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

## sha1sum
- SHA1 Checksum von Datei anzeigen:

```
sha1sum /path/to/file
```

- Vergleich von mehreren Hashwerten (funktioniert auch mit einem txt welches Hashwerte und entsprechende Paths zu den Files angibt )
```
sha1sum -c file1 file2
```

## Mount .img File in Linux
- /mnt/ Verzeichnis erstellen
```
mkdir /mnt/img
```

- .img File Informationen anzeigen lassen
```
fdisk -l disk.img
```

- Block-Size mit Startblock multiplizieren um offset herauszufinden
![[CleanShot 2022-10-12 at 10.28.29.png]]

- .img File mit korrektem offset mounten
```
mount -o loop,offset=1048576 disk.img /mnt/img
```

- Automtasiert mounten
```
sudo losetup -f -P disk.img
```

```
losetup -d/ dev/loop0p1
```

## sqlite
- Tool für Datenbanken zu vhescerwalten
- Kann zur Anonymisierung benutzt werden

### Syntax
- DB auswählen
```
sqlite3 data.db
```

- Tabellen anzeigen
```
.tables
```

- Spalten in Tabelle anzeigen
```
PRAGMA table_info('tablename');
```

- Inhalt von Tabelle anzeigen lassen
```
SELECT * FROM tablename LIMIT 10;
```

- Alle Zeichen mit Sternchen ersetzen bis auf erstes
	- substr(columname, 1(=Erstes Zeichen in Zeile), 1(= Anzahl Zeichen))
```
SELECT substr(columname, 1, 1) || '*********' FROM tablename LIMIT 10; 
```

```
UPDATE tablename SET columname = substr(columname, 1, 1) || '*********';
```

- Alle Zeichen mit Sternchen ersetzen bis auf letztes
```
SELECT substr('*********', 1, 9) || substr(columname, -1) FROM tablename LIMIT 10; 
```

```
UPDATE tablename SET columname = substr('*********', 1, 9) || substr(columname, -1);
```

- Spalte mit 10-Stelliger Zufallszahl ersetzen
```
SELECT abs(random()) % 1000000000 FROM tablename LIMIT 10;
```

```
UPDATE tablename SET columname = abs(random()) % 10000000000;
```


```
SELECT substr(abs(random()), 0, 11) FROM tablename LIMIT 10;
```

```
UPDATE tablename SET columname = substr(abs(random()), 0, 11);
```

- In einem Datum Tag und Monat entfernen
	- substr(columname, 1(=Erstes Zeichen in Zeile), 1(= Anzahl Zeichen))
```
SELECT substr(columname, 7, 4) FROM tablename LIMIT 10;
```

```
UPDATE tablename SET columname = substr(columname, 7, 4);
```


```
SELECT strftime('%Y', columname) from tablename;
```

```
UPDATE t_person SET date_of_birth = strftime('%Y', date_of_birth);
```

- Ersetzen von Werten mit einer Kategorie
```
UPDATE tablename SET columname = 'low' WHERE columname < 50000 AND columname NOT NULL;
UPDATE tablename SET columname = 'medium' WHERE columname >= 50000 AND columname < 100000 AND columname NOT NULL;
UPDATE tablename SET columname = 'high' WHERE columname >= 100000 AND columname NOT NULL;
```

- Werte aus Spalte löschen
```
UPDATE tablename SET columname1 = '', columname2 = '';
```

## strings
- Tool um strings von einem File auszugeben (Beispielsweise einer .exe)

### Syntax
- Beispielsyntax mit Filter
```
strings [EXE] | grep [FILTER]
```

## [wtfis](https://github.com/pirxthepilot/wtfis)
- Tool für Abfragen von Websites via CLI (beispielsweise Virustotal)

### Synatx
```
wtfis [URL]
```

## [name-that-hash](https://github.com/HashPals/Name-That-Hash)
- Tool to identify hashes

### Syntax
```
name-that-hash --text [Hash]
```

## [Starship](https://starship.rs/guide/#%F0%9F%9A%80-installation)
- Terminal Customization Tool

### Requirements
- [Nerd Font](https://www.nerdfonts.com/) 

### Install
1. `brew install starship`
2. `sudo nano ~/.config/starship.toml`
3. Use example-config ([for example](https://github.com/ChristianLempa/dotfiles-win))
4. `sudo nano ~/.zshrc`
```
[[ -f ~/.zsh/aliases.zsh ]] && source ~/.zsh/aliases.zsh
[[ -f ~/.zsh/functions.zsh ]] && source ~/.zsh/functions.zsh
[[ -f ~/.zsh/starship.zsh ]] && source ~/.zsh/starship.zsh
[[ -f ~/.zsh/nvm.zsh ]] && source ~/.zsh/nvm.zsh
[[ -f ~/.zsh/wsl2fix.zsh ]] && source ~/.zsh/wsl2fix.zsh

# Load Starship
eval "$(starship init zsh)"
source /opt/homebrew/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
```
5. `brew install zsh-syntax-highlighting` (Optional)
6. Change font in Terminal to a Nerd Font

### Activate in Warp terminal
![[CleanShot 2022-11-27 at 13.21.00.png]]