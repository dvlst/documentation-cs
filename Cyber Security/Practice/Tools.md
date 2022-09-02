# General
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

# Linux
## sha1sum
- SHA1 Checksum von Datei anzeigen:

```
sha1sum /path/to/file
```

- Vergleich von mehreren Hashwerten (funktioniert auch mit einem txt welches Hashwerte und entsprechende Paths zu den Files angibt )
```
sha1sum -c file1 file2
```


# Network
## Wireshark
- Paket-Basierte Proktolle anaylisieren
- Decodieren von Paketen
- Datenstorm Live ansehen

### Aufbau
1. Display Filter
2. Dekodierte Pakete
3. Protokollstack (Aufschachtelung)
4. Binäre Daten des Paktes

![[CleanShot 2022-08-08 at 20.17.25.png]]

### Filtern
- Pakete filtern
- [Liste von Displayfiltern](https://wiki.wireshark.org/DisplayFilters)
- Unter View > Internals > Supported Protocols
- Filter funktionieren mit Text / Hex / #RegEx
- Zulässige Vergleich:
	"== "(Gleich)
	"!=" (Ungleich)
	">" (Grösser)
	"<" (Kleiner)
	">=" (Grösser gleich)
	"<=" (Kleiner gleich)
	"~" (Matches)
	"&" (AND)
	"&&" (Logical AND)
	"||" (Logical OR)
	"^^" (Logical XOR)
	"!" (Logical NOT)

- Nach Client Hello filtern:
```
ssl.handshake.extensions_server_name
```

- Nach POST Requests filtern:
```
http.request.method == "POST"
```

- Nach GET Requests filtern:
```
http.request.method == "GET"
```

### Tipps
- Zertifikat exportieren:
	1.  "Server Hello, Certificat, Server Hello Done" Suchen (z. B mit `tls.handshake`)
	2. Rechtsklick "Export Package Bytes..." und Speichern als .crt

![[CleanShot 2022-08-29 at 20.12.05.png]]

- Private Key hinzufügen und Traffic entschlüsseln
- Unter Wireshark > Preferences > Protocols > TLS > RSA Keys den entsprechenden Private Key hinzufügen (.pem-File)

![[CleanShot 2022-08-29 at 20.48.53.png]]

## [tshark](https://tshark.dev/)
- Package anaylizer
- Kann live Network Traffic abhören
- Ähnlich wie Wireshark aber für Kommandozeile
- [pyshark](https://github.com/KimiNewt/pyshark) ist der Python-Wrapper für tshark

## [Scapy](https://scapy.readthedocs.io/en/latest/usage.html)
- Package anaylizer and manipulator
- Ähnlich wie pyshark aber kann Pakete verändern
- Kann zum Anonymisieren verwendet werden
- Scapy kann:
	- Pakete aufzeichnen
	- Pakete erstellen
	- Pakete anonymisieren
	- PCAP Files lesen
- Ist ein python modul

```
pip3 install scapy
```

## tcpdump

## ngrep

## dnscat2

## #nmap
- Host-Detektion
- Port-Scanning
- Dienste erkennen
- OS-Erkennung
- [nmap Cheat Sheet](https://www.stationx.net/nmap-cheat-sheet/)

## [Snort](https://www.snort.org/)
- Open Source Network Based Intrusion Detection
- Hört auf einem Netzwerkinterface
- Kann bekannte Netzwerkangriffe abwehren
- Snort vs #WAF
	- Snort ist gut für komplexe Regeln
	- WAF sind spezifisch für WebApplications / Snort ist für alle Netzwerk-Angriffe

### Modis
- alert - Löst Alarm aus
- log - Loggt Paket
- pass - Ignoriert Pake
- drop - Blockiert und Loggt
- reject - TCP-Reset oder unreachable bei UDP / ICMP
- sdrop - Block aber kein Log

### Rules
- Header
	- Aktion
	- Protokoll
	- Source-IP / Source-Port
	- Flow-Richtung
	- Destination-IP / Destination-Port
- Body
	- Konfiguration der Regel-Optionen
- Generelle Regeloptionen
	- Message - Nachricht was die Regel detektiert hat
	- Flow - Richtung des Netzwerkflusses definieren auf welchen die Regel reagieren soll
	- Reference - Auf externe Ressourcen verweisen
	- Classtype - Klassifizieren wie schwerwieghend eine erfolgreiche Attacke wäre
	- sid/rev - Snort ID / Revision Keyword um eine Regel zu spezifizieren
- Detecion Regeloptionen
	- Content - Für Inhalt in einem Payload suchen
		- distance/offset - Wo muss in dem Paket nach dem Payload gesucht werden
		- within/depth - Wie weit bei einem Content-Match weiter gesucht werden soll
	- PCRE - Erlaubt Regeln in #RegEx
	- Byte test - Erlaubt es nach einem Wert in Binär zu filtern
- Beispiel-Regeln:
```
alert tcp $EXTERNAL_NET any -> $HOME_NET any (
	msg:"MALWARE-CNC Win.Backdoor.Houdini variant
	screenshot inbound init command attempt"
	flow:to_client;
	content:"screenshot_init|0D 0A|";
	depth:17;
	offset:4;
	metadata:impact_flag red, policy balanced-ips drop[…] ruleset community;
	classtype:trojan-activity;
	sid:40833;
	rev:1;
)
```

```
alert tcp $EXTERNAL_NET any -> $HOME_NET $HTTP_PORTS

(
 msg:"SERVER-WEBAPP JavaScript tag in User-Agent field possible XSS attempt";
 flow:to_server,established;
 http_header;
 content:"User-Agent|3A| <SCRIPT>",fast_pattern,nocase;
 metadata:ruleset community;
 service:http;
 eference:url,blog.spiderlabs.com/2012/11/honeypot-alert-referer-field-xss- 
 attacks.html;
 classtype:web-application-attack;
 sid:26483;
 rev:2;
)
```

## [#ModSecurity](https://github.com/SpiderLabs/ModSecurity)
- Open Source #WAF (Web Application Firewall)
- Support für Apache / Nginx / IIS
- [Core Rule Set für ModSecurity](https://github.com/coreruleset/coreruleset)
	- Set von Regeln für bekannte Schwachstellen (z. B. #XSS / #SQLi)
	- Ab Version 3 "Anomalie Scoring"

### Funktionsweise
- Untersucht Requests nach Regeln
- 5 Phasen (bessere Performance da Body-Parsing aufwendig)
	- Request Headers
	- Request Body
	- Response Headers
	- Response Body
	- Logging

### Regeln
- Aufbau einer Regel: `SecRule VARIABLES "OPERATOR" "TRANSFORMATIONS,ACTIONS”`
- [Variablen](https://docs.huihoo.com/modsecurity/2.5.7/variables.html): Grobe Vorfilterung wo / wie man sucht
- [Operator](https://docs.huihoo.com/modsecurity/2.5.7/operators.html): Was und wie sucht man on den Variablen
- [Transformationen](https://nature.berkeley.edu/~casterln/modsecurity/html-multipage/06-transformation-functions.html): Verändern / normalisieren der gefilterten Daten
- [Actions](https://docs.huihoo.com/modsecurity/2.5.7/actions.html): Was passiert wenn Regel aktiv wird
- Beispiel-Regeln:

```
SecRule REQUEST_URI "@streq /admin.php" "id:1,phase:1,t:lowercase,deny”
```

```
SecRule ARGS_GET:username "@contains admin" "id:1,phase:1,t:lowercase,deny”
```

```
SecRule ARGS "@contains <script>" "id:1,deny,status:403,t:lowercase,t:removeWhitespace,t:htmlEntityDecode”
```

```
SecRule RESPONSE_BODY "@verifyCC \d{13,16}" "phase:4,id:1,t:none,log,capture,block,msg:'Potential credit card number is response body’”
```

### Anomalie
- Interne Schwellwerte bevor etwas geblockt wird
- Regeln blocken nicht direkt sondern erhöhen Score
- Regel checkt ob Anomalie-Score überschritten wurde

![[CleanShot 2022-08-15 at 20.45.14.png]]

![[CleanShot 2022-08-15 at 20.46.01.png]]


# Forensic
## [Volatility](https://www.volatilityfoundation.org/releases)
- Tool zum Memory Dumps analyisieren
- [Cheat Sheet Tools Volatility Commands](https://book.hacktricks.xyz/generic-methodologies-and-resources/basic-forensic-methodology/memory-dump-analysis/volatility-examples)
- [Volatility Command Reference](https://github.com/volatilityfoundation/volatility/wiki/Command-Reference)

### Volatility 2 install Windows
- Clone Repository from GitHub
```
git clone https://github.com/volatilityfoundation/volatility.git
```

- Make sure Python27 is installed
- Add Python27 to PATH System Variable (/Path/to/Python27/ & /Path/to/Python27/Scripts/)
- Rename python.exe (Python3) to python3.exe (%APPDATA%/Local/Programs/Python/Python310/)
- Install Visual C++ for Python27 from [Wayback Machine](https://web.archive.org/web/20190720195601/http://www.microsoft.com/en-us/download/confirmation.aspx?id=44266)

- Install distorm3 with pip
```
pip install distorm3
```
- Install pycrypto with pip
```
pip install pycrypto
```

### Volatility3 install Windows
- Clone Repository from GitHub
```
git clone https://github.com/volatilityfoundation/volatility3.git
```

- Install requirements
```
pip3 install -r requirements.txt
```

- If you have an C++ error you must install the [C++ Build Tools](https://visualstudio.microsoft.com/visual-cpp-build-tools/)
- Then you have to install the Desktop developement with C++

![[Pasted image 20220828213350.png]]

- If you get an Python-Snappy error while installing the requirements you have to install the python snappy module from the [Unofficial Windows Binaries for Python](https://www.lfd.uci.edu/~gohlke/pythonlibs/#python-snappy)
```
pip install \Path\To\python-snappy
```

- With this command you can show your supported version (cp310-cp310 worked for me):
```
pip debug --verbose
```

- You have to edit the requirements.txt to edit the python-snappy version:
```
...
python-snappy==0.6.1
```

- Install the symbols required for the different OS ([windows](https://downloads.volatilityfoundation.org/volatility3/symbols/windows.zip) [mac](https://downloads.volatilityfoundation.org/volatility3/symbols/mac.zip) [linux](https://downloads.volatilityfoundation.org/volatility3/symbols/linux.zip)) and unpack them into the /volatility3/volatility3/symbols/ folder

### Volatility3 Commands
- Show Info about the image
```
python3 vol.py -f memdump.raw windows.info
```

- Network Info from Windows
```
python3 vol.py -f memdump.raw windows.netscan
```

- Show Process Tree
```
python3 vol.py -f memdump.raw windows.pslist
```

- Show Hidden Processes
```
python3 vol.py -f memdump.raw windows.psscan
```

- Filter process tree after filename
```
python3 vol.py -f memdump.raw windows.pslist | Select-String filename
```

- Filter Windows Handles after PID
```
python3 vol.py -f memdump.raw windows.handles --pid 1328
```

- Filter Windows Handles after PID and type
```
python3 vol.py -f memdump.raw windows.handles --pid 1328 | Select-String File | more
```

- Dump all files associated with PID 3784.
```
python3 vol.py -f memdump.raw windows.dumpfiles.DumpFiles --pid 3784 |
```

- See executed programs with command option history.
```
python3 vol.py -f memdump.raw windows.cmdline.CmdLine
```

- See active network connections and listening programs.
```
python3 vol.py -f memdump.raw windows.netstat
```

- Dump the Windows user password hashes.
```
python3 vol.py -f memdump.raw windows.hashdump.Hashdump
```

- Print out the Windows Registry UserAssist.
```
python3 vol.py -f memdump.raw windows.registry.userassist.UserAssist
```

- List all available Windows Registry hives in memory.
```
python3 vol.py -f memdump.raw windows.registay.hivelist.HiveList
```

- Dump the ntuser hive based on a keyword filter.
```
python3 vol.py -f memdump.raw -o "dump" windows.registry.hivelist --filter Doe\ntuser.dat --dump
```

- Print a specific Windows Registry key.
```
python3 vol.py -f memdump.raw] windows.registry.printkey --key "Software\Microsoft\Windows\CurrentVersion" --recurse
```

- Print a specific Windows Registry key, subkeys and values.
```
python vol.py -f memdump.raw windows.registry.printkey --key "Software\Microsoft\Windows\CurrentVersion" --recurse
```

- Save memdump to a .dmp file
```
python3 vol.py -f memdump.raw windows.memmap.Memmap  --pid 368 -–dump
```

- ( Use Grep to find something in the .dmp file)
```
strings pid.368.dmp | grep "filename" | grep -v “filetype”
```

### Volatility2 Commands
- Show image information
```
python vol.py -f memdump.raw imageinfo
```

```
python vol.py -f memdump.raw kdbgscan
```

- Network Info from Windows
```
python vol.py --profile=Win7SP1x86_23418 netscan -f memdump.raw 
```

- Network Info from Linux
```
python vol.py --profile=SomeLinux -f memdump.raw linux_ifconfig
```

- Show Process Tree:
```
python vol.py -f memdump.raw --profile=Win7SP1x86 pslist
```

- Create a executable.exe file with PID
```
python vol.py -f memdump.raw --profile=Win7SP1x86_23418 procdump --dump-dir . -p 368
```

- Create a executable.exe with physical memory adress
```
python vol.py -f memdump.raw --profile=Win7SP1x86_23418 dumpfiles -Q 0x000000007dd6e038 -D .
```

- Search memdump after filename
```
python vol.py -f memdump.raw --profile=Win7SP1x86_23418 filescan | grep -i filename
```

- Search memdump after file-extension
```
python vol.py -f memdump.raw --profile=Win7SP1x86_23418 filescan | grep -i filename | grep -v filetype
```

- Search memdump after Windows Service Records
```
python vol.py -f memdump.raw --profile=Win7SP1x86_23418 svcscan
```

- Search memdump after COMMAND_HISTORY
```
python vol.py -f memdump.raw --profile=Win7SP1x86_23418 cmdscan
```

- Search memdump after CONSOLE_Informations
```
python vol.py -f memdump.raw --profile=Win7SP1x86_23418 consoles
```

### [MemProcFS](https://github.com/ufrisk/MemProcFS)
- Alternative zu Volatility für Windows
- Memory Dump in Laufwerk mounten:
```
MemProcFs.exe -device memory-dump.raw -forensic 1 
```

## log2timeline / [plaso](https://www.kali.org/tools/plaso/)
- Plaso-File aus vhdx oder memory dump erstellen
- vhdx-File mit Disk2vhd aus Sysinternals erstellen auf Windows
- Plaso-File erstellen:
```
log2timeline.py --storage-file *Name*.plaso *Name*.VHD
```

## [timesketch](https://github.com/kovakina/timesketch/blob/master/docs/SearchQueryGuide.md)
- Plaso-File anaylisieren mit GUI
- [Search query Guide](https://timesketch.org/guides/user/search-query-guide/)

## Memory Dump

## Cyberchef

## grep
- Filtern von Logs
- [Syntax](https://www.geeksforgeeks.org/grep-command-in-unixlinux/)


# Security
## #metasploit

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
- Advanced Inttrusion Detection Environment
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

## [Nessus](https://www.tenable.com/downloads/nessus?loginAttempted=true)
- Vulnerability Scanner
- Detection von Vulnerabilities
- Simliert Angriffe auf gewisse Vulnerabilities
- Führt Netzwerkscans aus
- Scannt nach Misconfigurations, Open Ports, DDOS Vulnerability, Passwords

## fail2ban
- Intrusion Prevention Tool
- Analyisiert Logfiles
- Blockiert IP bei definierter Anzahl Versuche in gewisser Zeitspanne

# Monitoring
## inotify

## checkmk

## Prometheus & Grafana

## #ELK Stack
- Zentralisiertes Logging System
- Kann mit #SIEM für Analyse erweitert werden
- Tool-Set für Sammeln von Logs aus mehrern Quellen
- Hilfreiches Tool für Reaktive Forensik
- KQL = Kibana Query Language
	- Abfrage-Sprache für Elastic Search Daten

### Bestandteile
- Beats
	- Liefert verschiedene Daten an Logstash
- Logstash
	- Verarbeitet / Normalisiert empfangene Logs und gibt diese anschliessend weiter
	- Inputs (empfangen) > Filter (normalisieren / aufbereiten) > Output (weiterreichen)
- Elastic Search
	- Such- und Analyse Maschine der vorhanden Daten
- Kibana
	- Visualisiert die vorhanden Daten und macht sie so einfacher auswertbar

### Ablauf
1. Daten werden über Beats geliefert
2. Logstash empfängt alle Daten und normalisiert diese und sendet diese weiter
3. Elastic Search sendet die Daten weiter
4. Kibana visualisiert die Daten

![[CleanShot 2022-08-23 at 20.32.36.png]]

## Splunk
- Vergleichbar mit #ELK

### Funktionen
- Sammelt Events
- Normalisiert und Indexiert Events
- Stellt Events dar

![[CleanShot 2022-08-23 at 20.43.19.png]]

## Links to other Tools
- [SANS Open Source Faculty Tools](https://www.sans.org/img/free-faculty-tools.pdf)
- [Microsoft Driver Analysis](https://www.microsoft.com/en-us/wdsi/driversubmission)
- [Parrot OS](https://www.parrotsec.org/)
- [#metasploit](https://www.metasploit.com/)
- [Log4J scanner](https://github.com/mergebase/log4j-detector)
- [Piracy Tools Reddit](https://www.reddit.com/r/Piracy/wiki/megathread/tools)
- [Virustotal](https://www.virustotal.com/gui/home/upload)
- [DES Cracker](https://crack.sh/)
- [Canary Tokens (Traps for Hacker)](https://canarytokens.org/generate#)
- [PwnDoc (Pentest Reporting)](https://github.com/pwndoc/pwndoc)
- [2FA for SSH](https://github.com/google/google-authenticator-libpam)
- [tcpdump](https://www.tcpdump.org/)
- [ngrep](https://github.com/jpr5/ngrep)
- [Open Source Network Visualizer](https://www.elastic.co/elastic-stack/)
- [Windows Sysinternals](https://docs.microsoft.com/en-us/sysinternals/)
- [john (Open Password encrypted .zip)](https://github.com/openwall/john/blob/bleeding-jumbo/src/zip2john.c)
- [ldapdomaindump: AD information via LDAP](https://github.com/dirkjanm/ldapdomaindump)
- [FEODO Botnet C&C servers](https://feodotracker.abuse.ch/)
- [radareorg: reverse engineering](https://github.com/radareorg/radare2)
- [Prometheus and Grafana (Monitoring Solution)](https://prometheus.io/docs/visualization/grafana/)
- [Checkmk (Monitoring Solution)](https://checkmk.com/)
- [Cyber Chef (Check possible Hashes etc)](https://gchq.github.io/CyberChef/)
- [GeoIP and other Tools](https://hackertarget.com/geoip-ip-location-lookup/)
- [MITRE ATT&CK Framework](https://attack.mitre.org/)
- [MITRE ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/)
- [inotify (Monitor files)](https://man7.org/linux/man-pages/man7/inotify.7.html)
- [Free Cyber Security Tools - CISA](https://www.cisa.gov/free-cybersecurity-services-and-tools)
- [Cyberchef | Decoding and Encrypting](https://gchq.github.io/CyberChef/)
- [dnscat2 | DNS Tunnel](https://github.com/iagox86/dnscat2)
- [Subnet Calculator](https://www.site24x7.com/tools/ipv4-subnetcalculator.html)
- [IP Lookup](https://www.maxmind.com/en/home)
- [Tails: Secure Linux](https://tails.boum.org/)
- [Coding in Browser](https://replit.com/)
- [#CVSS Calculator](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator)
- [#CVSS Alternative: BSI-Schwachstellenbeurteilung](https://www.bsi.bund.de/DE/Service-Navi/Abonnements/Newsletter/Buerger-CERT-Abos/Buerger-CERT-Sicherheitshinweise/Risikostufen/risikostufen.html)
- [Mail Spam Test](https://www.mail-tester.com/)
- [RegExr: Learn / Build / Test RegEx](https://regexr.com/)
- [Codepasting](https://paste.ofcode.org/)
- [Memory Dump (forensic / Timesketch)](https://timesketch.org/)
- [Threat Research](https://otx.alienvault.com/)
- [Decrypt Hashes](https://hashes.com/en/decrypt/hash)
- [Hacking-Lab VM](https://livecd.hacking-lab.com/)
- [HexEd.it](https://hexed.it/)
- [#CIS-Benchmark](https://www.cisecurity.org/cis-benchmarks/)
- [Stig Benchmark](https://www.stigviewer.com/stigs)
- [OpenVAS | Vulnerability Scanner](https://www.openvas.org/)
- [Cuckoo Sandbox](https://cuckoosandbox.org/)
- [ghidra: Software Reverse Engineering](https://github.com/NationalSecurityAgency/ghidra)
- [AlienVault | Open Source Threat Intelligence](https://otx.alienvault.com/)
- [spiderfoot | Automated OSINT](https://www.spiderfoot.net/)
- [Threat Intelligence Tool](https://pulsedive.com/)
- [Open Source Threat Intelligence Tools](https://www.misp-project.org/)
- [Insecure WebApplication - Webgoat](https://owasp.org/www-project-webgoat/)
- [py2exe](https://stackabuse.com/creating-executable-files-from-python-scripts-with-py2exe/)
- [WinPrefetchView](https://www.nirsoft.net/utils/win_prefetch_view.html)
- [Store Encryption Keys securely](https://www.vaultproject.io/)
- [Man in the Middel - 2FA umgehen mit Reverse Proxy](https://github.com/kgretzky/evilginx2)
- [Cipher Suite Info](https://ciphersuite.info/cs/)
- [SQLite Viewer](https://inloop.github.io/sqlite-viewer/)