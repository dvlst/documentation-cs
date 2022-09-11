# Detection
## Im Netzwerk
- Sensoren / Monitoring
- Traffic zwischen Hosts
- Network Firewall / #WAF 
- Malwarecheck auf Mail-Gateway
- [#Forward-Proxy](https://www.jscape.com/blog/forward-proxy-vs-reverse-proxy)
- Logs analyisieren

## Auf Host
- Sensoren / Monitoring
- Auf allen Hosts (Workstation, Notebook, Server, Network Devices)
- Antivirus Software
- OS Integrity-Check
- Local Firewall
- File Überwachung
- Logs analyisieren

## Muster
### Relevante Muster
- Geolocation (IP)
- [Payload](https://www.malwarebytes.com/glossary/payload)
- Mail-Adressen
- Network-Traffic (Size, Source > Destination, #Lateral-Movement)
- Biometrische Muster (Tippgeschwindigkeit)
- Signatur von Dateien
- #Process-Tree

![[CleanShot 2022-08-07 at 13.33.14.png]]

### #CRS (Core Rule Set)
- OWASP #ModSecurity CRS - Detection von Attacken auf der WAF
- Beispiele für Injection:
	- #SQLi - SQL Injection
	- #XSS - Cross Site Scripting
	- LFI - Local File Inclusion
	- RFI - Remote File Inclusion 
	- RCE - Remote Code Execution
	- PHP Code Injection  
	- HTTP Protocol Violations

### Hidden Pattern
- VPN für Geolocation
- Zufällige Timeouts für Biometrische Muster
- Malware Neu Kompilieren um Signatur zu Umgehen
- Entfernen von Artefakten in Logs

### Regeln
- Verknüpfen von Mustern
- Kombinieren von Logischen Ausdrücken
- Regeln = Nicht intelligent
- Beispiele:
	- 3 fehlgeschlagene Logins in 60 Minuten
	- Input beginnt mit ```<script>```
	- E-Mail hat .zip-Anhang

### Anomalie
- Definieren von Baseline
	- Requests / Tag
	- Logins / Tag

![[CleanShot 2022-08-07 at 14.15.53.png]]

### Machine Learning
- A.I nutzen um Regelset aufzubauen
- Hidden patterns können durch A.I detected werden
- Algortihmen lernen
	- Bekannte Malware
	- Anomalien
	- Verhalten

### #Logs
- Windows Event Viewer
	- Sicherheit, System, Applikation
	- Export nach CSV, XML, EVTS möglich
- Linux (/var/logs)
	- Textdateien
	- Sammelbar mit [```journalctl```](https://man7.org/linux/man-pages/man1/journalctl.1.html)

## Tools
### Firewall
- Trennung von Netzwerkzonen
- OSI-Layer 4
-  Kann angriffe detektieren (Portscans, #DDOS, #Lateral-Movement)

### Packet-Inspection
- Pakete analyisieren / #DPI - Deep Packet Inspection
- Erkennen von (Malaware, #C2 Connections, Spam)
- Nachteile: Performance, Privatsphäre
- #Reverse-Proxy / #Forward-Proxy

### Integrity Check
- Host / Netz: Malware-Signatur detektieren
- Host: Veränderungen am Dateiinhalt detektieren
- Nachteile: Kann manipuliert werden, Baseline ändert sich mit neuen Installationen
- Checksum Verification (Dateien vergleichen anhand von Hashwerten)

### Process-Monitoring
- Prozesse können Sub-Prozesse starten
- #Process-Tree analyisieren um alle Sub-Prozesse zu finden
- Detektieren von verdächtigem Verhalten
	- Starten von Sub-Prozessen
	- Ausnutzen von Exploits
	- #C2 Verbindungsaufbau
	- Zugriffe auf Files / Registry
- Wird bestenfalls in Sandbox gemacht

## #IoC 
- Indicators of Compromise
- Artefakte welche bei einem Angriff hinterlassen werden
- Reaktive (während oder nach Angriff)
- Regeln / Muster / Detection:
	- IP-Blacklist
	- Paketgrösse monitoren
	- #DPI - Deep Packet Inspection
	- #Forward-Proxy
	- Admin-Flag monitoren
	- Geo-IP monitoren
	- Login-Funktion monitoren
	- Ausgehender Traffic Monitoren ( #Forward-Proxy )
	- Threshold bei failed Logins
	- Network-Traffic monitoren
	- DB-Logs monitoren
	- Web-Logs monitoren
	- Baseline-Zustand in Sandbox
	- Shares monitoren
	- Anti-Virus / Manuelle / Unüblichbes Verhalten von Subprozessen

### Network
- Traffic an Malware-Domain / IP
- Traffic von System welche nicht nach aussen kommunizieren
- Grosse ausgehende Datenmengen

### User
- Standard User wird Domain-Admin
- Standard User hat Admin-Rechte in Web-Applications

### Geolocation
- Plötzliche Änderung der Geolocation der Requests

### Logins
- Viele fehlgeschlagene Logins = Bruteforce
- Viele fehlgeschlagen und ein erfolgreicher Login = Kompromittierung

### Datenbanken
- Lesezugriff nimmt zu
- #SQLi / Weak Configuration kann zu Angriff führen

### Files
- Login File in Web Application hat vielle Zugriffe

### Ports
- Benutzen von unüblichen Ports um sich vor Intrusion-Detection-System zu verstecken
- Zum Beispiel:
	- SSH über Port 80
	- #DNS-Tunneling

### Registry-Einträge / Systemfiles
- Verdächtige Einträge in ``/etc/hosts```
- Malware in Autostart

### Ungeplante Patches
- System ist plötzlich gepatcht
- Angreifer schliesst Sicherheitslücke hinter sich
	- #EternalBlue

### Daten an unüblichen orten
- Verdächtige Daten auf Shares oder ```%TEMP%```, ```C:\```

### Malware auf System
- Malware auf System zurückgelassen
- Ransomware > Dateien verschlüsselt > Viele Schreibzugriffe auf Dateien

## #IoA
- Indicators of Attack
- Proaktiv (während oder bevor Attacke)
- Unterbinden von Angriffen bevor sie passieren
- Beispiele:
	- Portscanning
	- Unübliche DNS-Abfragen
	- Unübliche Restarts von Hosts
	- Unübliche offene Ports auf Hosts
	- Passwortänderungsversuche
	- Hoher Traffic auif gewissen Protokollen (SSH)
	- Installationsversuche von komischer Software
- Bedingt Live Logging / Analyse

## Intrusion Detection
- #IDS = Intrusion Detection System

### Host Based Intrusion Detection
- Host haben #IDS installiert welche mehrere Kategorien überwachen
- Signatur Basierte Erkennung
	- Antivirus / Root-Kit-Detection
	- SNORT-Regeln
- Anomalie-Detektion
	- Verhaltensveränderung (z. B Process-Spawning > Subprocesses)
	- Ungewöhnliche Zugriffe auf Daten / Programme
- Logs Auslesen (um Angriffe zu erkennen)
- Lokalen Netzwerk-Verkehr überwachen
	- Lokale Firewall

![[CleanShot 2022-08-22 at 19.03.10.png]]

- Beispiel #AIDE, #OSSEC, TripWire, Samhain

### Network Based Intrusion Detection
![[CleanShot 2022-08-22 at 19.03.36.png]]

## Threat-Hunt
- Eher reaktiv ( #SIEM, #IoC )
- Bedrohungen finden bevor schaden zu gross
- Bedrohungen identifizieren / isolueren
- Iterativer Prozess
- Artefakte aus #IoC / #IoA
- #Framework wird verwendet

### Threat Hunting Framework
1. Übersicht beschaffen (Inventar, Netzwerkplan)
2. Bedrohungsanalyse ( #MITRE )
3. Hypothese formulieren (Wie geht Angreifer vor?)
4. Threat-Hunt planen
5. Ausführung / Datenanalyse
6. Events untersuchen
7. Analyse verändern / Feedback Loop

![[CleanShot 2022-08-07 at 15.49.32.png]]

### SANS Abstufungen
1. Initial - Level 0 (Automatisiertes Reporting, keine Datensammlung)
2. Minimal - Level 1 (Threat Intelligence Indicator Search, Moderate Datensammlung)
3. Procedural - Level 2 (Datennalyse Prozeduren von anderen folgen, Hohes Level an Datensammlung)
4. Innovative - Level 3 (Eigene Datenanalyse Prozeduren, Sehr Hohes Level an Datensammlung)
5. Leading - Level 4 (Automatisierte Datenanalyse Prozeduren, Sehr Hohes Level an Datensammlung)

## #TTP
- Tactis, Techniques and Procedures
- Versuch den ganzen Eisberg zu formulieren
	- Bad News nur Spitze des Eisbergs
- Erfahrungen aus angriffen sammeln
- Tactics
	- Was möchte der Angreifer erreichen?
	- Beispiele: Impact, Exfiltration, Defense Evasion
- Techniques
	- Wie wiell der Angreiffer das erreichen?
	- Beispiele: Hooking, #ReverseShell

### Muster von Angriffen
1. Auskundschaften / Informationen sammeln
2. Schwachstellen ausnutzen
3. Host übernehmen
4. Verbreitung / Persistenz
5. Datenzugriff
6. Datenabzug

- Beispiel #APT Zyklus

![[CleanShot 2022-08-07 at 16.10.11.png]]

- Beispiel Penetration Test

![[CleanShot 2022-08-07 at 16.11.26.png]]


# Cyber Security Domains
### Threat Intelligence
- Externel / Internal
- Contextual / Inteligent Sharing

### User Education
- Training (new skills)
- Awareness (reinforcement)

### Security Operations
- Active Defence
- Incident Response
- #SIEM
- #SOC
- Protection
- Detection

### Career Developement
- Training
- Certification
- Self Study

### Security Architecture
- Secure System Build
- Cryptography
- Access Controll
- Network Design
- Data Protection

### Physical Security
- Physical Network Separation
- Access Control to Hardware Components

### Risk Assessment
- Penetration Test
- Vulnerability Scan
- Blue Team / Red Team

### Governance
- Laws and Regulation
- #KPI / #KRI
- Audits
- Risk informed

# Informationssicherheit
### Motivation / Ziele
- Geopolitische Einflussnahme
- Ideologische Ziele
- Industrielles Umfeld
	- Daten entwenden
	- Daten manipulieren
	- Betrieb stören
	- Zahlungen auslösen
	- Rufschädigung
	- Follow the Money
- Angriff auf andere Organisationen

### Angriffs-Vektoren
- Cloud Computing
- Mobile Devices Security
- Network Applications
- Lack of Cyber Security Specialists
- Botnets
- Insider Threats
- Social Networking
- Unpatched Software

# Bedrohungsarten
### Allgemeines
- Absolute Sicherheit gibt es nicht
- Ziel = Risiko reduzieren
	- Risiko = Wahrscheinlichkeit x Schaden

### Ohne Vorsatz
- Höhere Gewalt (Feuer, Blitz, Wasser)
- Fahrlässigkeit (Irrtum, Fehlebedienung)
- Technisches Versagen (Stromausfall, Hardwareausfall)

### Mit Vorsatz
- Manipulation
- Hacking
- Spionage
- Sabotage
- Organisatorische Mängel (Unberechtigter Zugriff, Ungeschultes Personal)

## #Denial-Of-Service
### Ziele
- Dienste Stören
- Geld-Erpressung
- Vandalismus
- Rufschädigung
- Konkurrenz stören

### [SYN flood](https://www.imperva.com/learn/ddos/syn-flood/)
- TCP #3-Way-Handshake ausnutzen
- TCP #3-Way-Handshake
		1. SYN (Client > Server)
		2. SYN-ACK (Server > Client)
		3. ACK (Client > Server)
- Angreifer sendet SYN Requests an alle offenen Ports
- IP-Adressen sind oftmals gespooft
- Server antwortet mit SYN-ACK, Client sendet aber nie ACK weswegen die Verbindung ausgelastet wird

![[Pasted image 20220803200825.png]]

### DNS / #NTP-Amplification
- Durch Requests werden grössere Antworten ausgelöst
- IP-Adresse wird gespooft
- DNS Amplification
	- Kleine Anfragen für Grosse DNS Records
	- Als Adresse für Antwort wird diejenige des Opfers angegeben
- NTP Amplification
	- NTP = Network Time Protocol
	- Zeitserver für das synchronisieren der Uhr über das Internet
	- Mit kurzer Anfrage werden die letzten 600 IP-Adressen welche sich zum Zeitserver verbunden haben freigegeben (monlist command)
	- Antwort ist 200 mal grösser als Anfrage
1. Mithilfe Botnetz und gespooften IP-Adressen werden UDP Pakete an Server gesendet
2. Jedes UDP Paket macht einen Request an NTP Server für den monlist command
3. Der Server antwortet der gespooften Adresse mit den geforderten Daten
4. Grosse Datenmengen durch die Requests können das Opfer lahmlegen

![[Pasted image 20220803201839.png]]

### #Slowloris
- Verwendet HTTP-Requests um mehrere Verbindung zu Server aufzubauen & offenzuhalten
- Kleine Bandbreite mit viel Ressourcen
1. Viele nicht abgeschlossene HTTP Request Headers werden an Zielserver gesendet
2. Der Zielserver öffnet eine Thread für jede Request
3. Damit kein Timeout passiert werden regelmässig weitere Requests geschickt
4. Der Zielserver kann die nicht abgeschlossenen Verbindungen nicht schliessen. Wenn alle Threads ausgelastet sind kann der Zielserver keine weiteren Anfragen annehmen

![[Pasted image 20220803203228.png]]

### Distributet Denial-Of-Service
- Attacker verwendet Botnetze für Grosse Auslastung des Opfers

![[CleanShot 2022-08-03 at 20.33.22.png]]

## Social Engineering
- Manipulieren durch Menschliche Handlungen oder Täuschung
- Mails, Social Media, Telefonanrufe (Vishing)
- Funktioniert aufgrund negativer Emotionen (Angst) oder aufgrund personenbezogener Informationen (Vertrauenswürdige Namen)
- Authorität wird vermittelt (meist CEO, Regierung oder Bank)

### Phishing
- Mail mit gefährlichen von angeblich grossen Firmen (Amazon, Microsoft, Netflix)
- Gefälschte Login Websiten zu bekannten Diensten (Office, Google)
- Spear Phishing (gezielte Attacken / Kontextbezogen)

### Malware-Dropper
- Word / Excel Makros welche Schadsoftware nachinstallieren
- Mail-Anhänge welche Schadsoftware beinhalten
- USB-Drop

### Andere Techniken
- Dumpster Diving
- CEO-Fraud
- Piggy-Backing

## Malware
- Software mit Absicht Daten zu stehlen / manipulieren / abzuhören

### Trojaner
- Tarnt sich als Seriöse Software
	- Office-Makros
	- Virenschutz
- Eigenschaften
	- Ausführen beliebiger Befehle
	- Nachladen weiterer Schadsoftware
	- Entwenden von Daten
	- Daten löschen
	- Weiter Verbreitung
- RAT - [Remote Access Trojan](https://hackersterminal.com/what-is-remote-access-trojan/)
	- Infizierte Clients werden als Server verwendet um sich auf den #C2 Server (Client) zu verbinden
- #ReverseShell zwischen Opfer und Angreifer wird aufgebaut
![[CleanShot 2022-08-03 at 21.09.26.png]]
- [Emotet](https://www.malwarebytes.com/emotet)
	- Nutzt Mails zur Verbreitung
	- Lädt mit Makros Schadsoftware nach
	- Verbreitet sich selbst wie Wurm
	- Ziel war es Informationen abzufangen
	- Kann mit anderer Malware (wie beispielsweise Ransomware) kombiniert werden
	1. Opfer erhält E-Mail mit Word-Anhang
	2. Opfer öffnet Anhang
	3. Makro-Warnhinweis wird ignoriert
	4. Makro lädt Emotet nach
	5. Emotet lädt Trickt nach
	6. Trickbot infiziert andere Systeme über EternalBlue
	7. Angreifer installieren Ryuk Ransomware über #C2 Server
	8. Ransomware wartet solange im Netz bis alle Backups verschlüsselt sind

### Wurm
- Reproduziert sich selber
- Ziel ist Verbreitung im Netzwerk
- Nach Infektion > Verbindung mit #C2 Server
- LOVELETTER
	- VBS-Skript als Mailanhang
	- Sendet sich selber an alle Outlook-Kontakte
	- Durchsucht Computer nach Passwörtern
- [Stuxnet](https://www.cyber.nj.gov/threat-center/threat-profiles/ics-malware-variants/stuxnet)
	- Militärischer Einsatz
	- Zerstörte Hardware durch manipulation der zentralen Steuerrungssoftware

### Ransomware
- Erpressungssoftware
- Verschlüsselt Dateien
- Verlangt Geld
- WANACRY / PETYA
	- Nutzt [EternalBlue](https://www.sentinelone.com/blog/eternalblue-nsa-developed-exploit-just-wont-die/) Schwachstelle um System zu infizieren
	- Nutzte Sicherheitslücke im SMB Protokoll aus

### Angriffe auf Webanwendungen
- OWASP konzentriert sich auf Webapps
- #XSS (Cross Site Scripting)
	- Über Eingabefelder kann Code auf Webservern ausgeführt werden
	- ```<script>alert(1)</script>``` zum testen
- #SQLi - SQL Injections
	- SQL Code bei Anfrage (z. B. Eingabefelder) übertragen welche dann ausgeführt wird

### APT (Advanced Persistent Threats)
- Gezielte Angriffe auf Organisation
- Lange Vorbereitungszeigt / Viel Geduld
- Verschiedene Angriffstechniken
- Persistenz (Verschiedene System)
	- Angreifer will nicht endteckt werden bis möglichst viele Systeme infiziert sind
- #Lateral-Movement (Im Netz ausbreiten)
	- Client 1 > Client 2 > Anwendungs-Server > Domain Controller 

![[Pasted image 20220803213602.png]]

## #Framework
### #NIST Cyber Security Framework
![[Pasted image 20220803193935.png]]


### IKT-Minimalstandard
- Übersetzung des NIST Cyber Security Frameworks
- Wird von Bund verwendett

### PPT Framwork
- Processes People Technology

![[CleanShot 2022-08-03 at 19.43.02 1.png]]

# Daten
## Austauschformate
- Austausch von Daten zwischen heterogenen System (bspw. SIEM)
- Verschiedenen Datenquellen liefern verschiedene Arten von Daten
	- Logs, Config-Fikes
	- Binäre Daten (Word-Dokumente, Bilder)

## Datenstrukturen
### Unstrukturierte Daten
- Unorganisiert
- Kein bestimmtes Format
- Kann nicht in DBs dargstellt werden
- Viel Speicherplatz
- Beispiele:
	- Bilder / Videos
	- Text
	- Kommentare
	- E-Mails
	- Logfiles (teilweise)
- Grössere Datenmengen / Big-Data

### Strukturierte Daten
- Feste / Maschinengenerierte Daten
- Kann in Tabellen / DBs dargstellt werden
- Eher wenig Speicherplatz
- Beispiele:
	- SQL-Tabellen
	- CSV-Files ohne Header

### Semi-Strukturierte Daten
- Daten definieren Struktur
- Struktur kann sich ändern
- Beispiele:
	- XML
	- JSON
	- CSV-Files mit Header

## CSV
- Comma Separated Value
- Semi-Strukturiertes Text-Forma
- Komma repräsentiert Spalte
- Erste Zeile ist Spaltenbezeichnung
- Kann gut Tabellen darstellen

### Schwachstellen
- Kommas / Newline können eventuell in Injection-Angriffen augsgenutzt werden

## XML
- Extensible Markup Language
- Semi-Strukturiert
- Kann als Baum dargestellt werden
- XML-Basierte Datenformate
	- HTML
	- SVG
	- SAML
- Beinhaltet:
	- Tag
	- Attribut
	- Element

### Aufbau
```
<tag>
	<element attribut="attribut1">
		Inhalt
	</element>
</tag>
```

### Eigenschaften
- Dokument ist "Wohlgeformt"
	- Besitzt ein Wurzelelement (Tag welcher alles umschliesst)
	- Alle Elemente haben Start und Endtags
	- Elemente haben nicht mehrere Attribute mit dem selben Namen
	- Case-Sensitive

### Nachteil
- Besitzt grossen Overhead (Zusatzinformationen welche nicht zu den Nutzdaten zählen)

## JSON
- JavaScript Object Notation
- Kompaktes Format
- Geignet zum Austausch von Daten zwischen Server und JS-Client
- Elemente:
	- NULL
	- Boolean
	- Integer / Float
	- Strings
	- Arrays
	- Objects
- Kann keine Binärdaten enthalten

### Aufbau
```
{
	"Wert1": "Text"
	"Wert2": 2e+6
	"Wert3": true
}
```

## YAML
- YAML Ain't Markup Language
- Menschenlesbare Daten-Serialisierungs-Sprache
- Serialisierung = Umwandlung eines Objekts in Folge von Bytes zum abspeichern oder versenden
- Besteht aus:
	- Skalaren (Strings, Integer, Floats)
	- Listen
	- Assoziativen Arrays (z. B. Dictionaries)

### Aufbau
- "#" sind Kommentare
- "-" sind Listen
- ```key:value``` = Assoziatives Array
- " ' = Strings
- | > = Skalare / Block Skalare über mehrer Zeilen
```
---
Element1:   Wert1
Element2:   Wert2

Liste1:
	- Element1-1:   Wert1-1
	  Element1-2:   Wert1-2

	- Element2-1:   Wert2-1
	  Element2-2:   Wert2-2
```

## Klassifizierung
- Unternehmen Klassifzieren oft Daten um diese zu schützen:
	- Öffentliche Daten (Zugänglich für alle)
	- Interne Daten (Nur für interne Mitarbeiter, Bspw. Telefonverzeichnis)
	- Vertrauliche Daten (Nur für gewissen Mitarbeiterkreis, Bspw. Mitarbeiterdossier)
	- Geheime Daten (Grosser Schutz / Sehr sensitiv, Bspw. Kundendaten)
- Anforderungen sind oftmals reguliert oder gesetzlich geregelt
- #IDS / #IDP / Data-Loss-Prevention muss oftmals Angriff auf
	- z. B. #WAF Regele welche Kreditkarten-Abfluss detektieren soll

## Status
### Data in Use
- Daten welche in Programmen verarbeitet werden
- Daten in volatilen Speichern (CPU-Register, RAM)
- Daten in temporärern Dateien
- Sollten geschützt werden da sie von jedem gelesen werden können
- Daten in Laufzeit schützen:
	- Dafür sorgen das diese nicht im Speicher bleiben (Denn diese können z. B mit Coredumps / Memorydumps und Tool wie Volatility aus dem Speicher gelesen werden)
	- Bspw. Java (Strings "Immutable", einmal erstellt können sie nicht mehr verändert werden)
	- z. B. Garbage Collector räumt irgendwann nicht referenzierte Strings auf
- Beispiele:
	- Office-Apps
	- PDFs
	- DBHs
	- Cloud Apps

### Data in Transit
- Daten in temporärern Dateien
- Beispiele:
	- E-Mail-Attachement
	- Downloads / Uploads
	- LAN Transfers
	- VPN
	- Messaging

### Data at Rest
- Daten folgendermassen schützen:
	- Verschlüsseln
	- Zugang regulieren (Daten Klassifizieren, Policy erstellen)
- Wo können Daten verschlüsselt werden?
	- Auf DB Server > Disk Encrypton
	- Auf DB selber (z. B. SQLCipher für SQLite)
- Wo sind Schlüssel gespeichert?
	- Hardware Security Module / Trusted Platform Modules
- Wie Schützen?
	- USB-Drive (Verschlüsselte Partition / ZIP / Image)
	- Mobile-App (File Based Encryption (Daten verschlüsseln aber Metadata nicht))
- Beispiele:
	- File Server / Network Share
	- DMS
	- Desktops / Laptops
	- USB-Drives

# Anonymisierung
- Das verändern personenbezogener Daten das diese nicht mehr Zugeordnet werden können
- Pseudoanonymisierung = Kann mit Rohdaten verlinkt werden und wieder hergestellt werden

## Was wird anonymisiert?
- Log-Files
- Network-Traffic
- Fehlermeldungen
- Archivierung
- Forschungsergebnisse
- Daten vor dem hochladen in die Cloud

## Welche Daten werden anonymisiert?
- Direkte Identifier
	- Name, Adresse, Telefonnumer
- Indirekte Identifier
	- Geburtstag
	- Geschlecht
	- Postleitzahl

## Methoden
- Anonymisierung
	- Löschen von Daten
	- Maskieren von Daten
- Pseudo-Anonymisierung
	- Verschlüsseln
	- Ersetzen durch Index

# Honeypots
- Intrusion Detection Tool
- Falle für Angreifer
- Verhalten von Angreifer beobachten
- Honeynets = Verbund von Honeypots

## Motivation
- Muster von Angriffen erkennen
- IP-Adressen blockieren
- Verhalten von Malware erforschen

## Klassifizierung
- Physische Implementierung
	- Echte Maschinen
	- Hohes Interaktionslevel
	- Komplexe Anwendungen simulieren
- Virtuelle Implementierung
	- Simulieren Verhalten von Diensten
	- Tiefes Interaktionslevel
- Hohe Interaktion
	- Komplettes Betriebsystem
	- Schwierig für Angreifer herauszufinden
	- Komplexes Deployment
	- Risiko das Maschine wirklich kompromittiert wird
- Tiefe Interaktion
	- Limitierte Funktionalität (z. B. Fake Filesystem)
	- Einfaches Deployment
	- Risiko das System kompromittiert wird ist kleiner

# Testing
- Ziel: Effektivität von Detection Massnahmen testen / erforschen / verbessern

## Use-Cases
- Mögliche Testszenarien:
	- #WAF 
	- Antivirus
	- Spamfilter / Phishing filter
	- #IDS 
- Was wird getestet:
	- Effizienz der Regeln
	- Was wird detected? Was wird nicht detected?

## Anomalie
- Ungewöhnlicher Anstieg einer gewissen Aktivität in einem gewissen Zeitraum
- z. B. ungewöhnlich viele Login-Versuche und danach plötzlich keine mehr

![[Pasted image 20220823194429.png]]

## False Positive
- Falsche Alarme

### Beispiele
- Inventar Programm mach Port-Scans
- Datei wird als fälschlicherweise Virus identifiziert
- Threshold (Triggerpunkt vonist falsch konfiguriert
- Software-Zertifikat fehlt

### Konsequenzen
- E-Mails werden gelöscht
- "Alert-Fatigue" bei Analysten
- Falsche Alarmmeldung bei Kunden

## False Negative
- Angriff wird nicht detektiert

### Beispiele
- Bypass einer #WAF Regel
- Analyst schätzt Alarm als False Positive ein
- Spam-Mail kommt durch

## Verhindern von False Positives / Negatives
- #IDS / #IDP Lösungen gut konfigurieren
- Iterative Regeln kontinuierlich anpassen / verbessern
- Thresholds kontinuierlich anpassen
	- Threshold = Trigger / Schwellwert bis Alarm ausgelöst wird
- White-Listing

![[CleanShot 2022-08-23 at 20.01.10.png]]

## Testen von Applikationen
- Penetration Test

### Ziel
- Tiefgehende Schwachstellen / Konfigurationsfehler finden
- Applikation genau untersuchen
- Enger Scope
- In Applikation eindringen

### Beispiele
- Web-Anwendung
- #WAF Regelwerk
- #IDP Regelwerk
- Zutrittssystem

## Testen von Organisationen
- Red Teaming

### Ziel
- Testen der allgemeinen Sicherheit
- Simulierter Angriff auf die ganze Firma
- Breiter Scope
- In Unternehmen eindringen

### Beispiele
- Phishing
- Social Engineering
- Interner Angriff
- Malware-Infektion

# Zentralisiertes Logging
- Logs werden an zentraler Stelle gesammelt und visualisiert
- #SIEM
- Tools wie #ELK oder #Splunk
- Aufbewahrungsdauer = Retention Time

### Ziele
- Schnell handeln können bei einem Vorfall
- Abfragen über mehrere System machen
- Logs müssen nicht mühsam zusammengesucht werden

## Security-Logging
- Möglicht viel und Möglichst lange Loggen für gute Nachvollziehbarkeit

### Was soll geloggt werden?
- AD
- Reverse / Forward Proxy
- VPN
- E-Mail Gazteway
- Host Security Logs
- Endpoint Security
- DNS
- Firewalls
- Drucker
- Alle Netzwerkgeräte
- IoT

### Was soll nicht geloggt werden?
- Quellcode
- Session-Infos
- Tokens (Access, Refresh, ID)
- Personenbezogene Daten
- Passwörter
- DB-Connection Strings
- Kontoinformationen
- Daten welche höher klassifiziert sind

## #SIEM 
- Security Information and Event Management
- Sammelt, Analysiert und zentralisiert Logs von allen Network Devices
- Erweiterung einer zentralisierten Logging Lösung wie ELK Stack oder Splunk
- Echtzeitanalyse der Events basierend auf Mustern und Regelen
- Echtzeit-Alarmierung
- Erstellung von Reports

### Wie vorgehen?
- Regeln /  Trigger setzen
- Muster kennen
- False Positives behandeln
- Regeln koninuierlich warten

## #SOC 
- Security and Operations Center
- Abteilung einer Firma / Externe Firma welche sich nur um Analyse von Events kümmert
- Oft zentralisiert bei grösseren Firmen