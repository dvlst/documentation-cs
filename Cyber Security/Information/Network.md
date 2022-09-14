# #OSI
- Open Systems Interconnection Model
- TCP/IP-Referenz-Modell = Vereinfaches OSI Modell

![[CleanShot 2022-08-08 at 19.24.03.png]]

- TCP/IP-Referenz-Modell ist verschachtelt

![[CleanShot 2022-08-08 at 19.26.35.png]]

# Protocols
## Ethernet / MAC
- #OSI Layer 1/2
- Protokoll-Sammling von Standards auf Hardware und Software
- In lokalen Netzwerken
- Nicht zuverlässig / Keine Sicherheit / Keine Authentisierung

### NAC = Network Access Controll
- Sichere Authentisierung in einem Netz
- Einschränkung des internenen Netzes für Gäste 
- Zertifikatbasiert

## IPv4/IPv6
- Grundlage des Internets
- Routable
- Netzwerke können miteinander verbunden werden
- Aufteilung in Netz und Host (Subnetzmaske)
- CIDR-Notation: 10.0.0.0 - 10.255.255.255 = 10.0.0.0/8

![[CleanShot 2022-08-08 at 19.50.05.png]]

## ICMP
- Internet Control Message Protocol
- Für Verfügbarkeitscheck von Hosts / Ports 
- Ping

## UDP
- User Datagram Protocol
- UDP ist verbindunglos (Pakete sind unabhängig)
- UDP ist nicht losless / zuverlässig
- Wenn Checksum fehlschlägt wird Paket verworfen
- Vorteile: Einfach, Schnell, Lightweight

## TCP
- Transmission Control Protocol
- Zuverlässig
- #3-Way-Handshake

## DHCP
- Dynamic Host Configuration Protocol
- Beinhaltet IP-Adresse, Subnetzmaske, Standard Gateway, DNS-Server
- Kann manuell konfiguriert werden
- DHCP-Server verwaltet Netzwerkonfiguration

### Ablauf
1. Client fragt Broadcast-Adresse an
2. Der schnellste DHCP Server wird verwendet
3. Host frag Konfiguration an
4. Server sendet Daten

## DNS
- Domain Name System
- Weist IP-Adressen Namen zu
- DNS Server löst Namen auf

### Records
- A-Record = Weist Namen einer iPv4-Adresse zu
- AAAA-Record = Weist Namen einer iPv6-Adresse zu
- MX-Record = Weist Namen einem Mail-Server zu
- TXT-Record = Weist Namen einem Text zu

## LDAP
- Lightweight Directory Access Protocol
- Wird in Verzeichnisdiensten verwendet

## File-Transfer-Protocols
- Network File System (NFS)
- Server Message Block (SMB)
- File Transf Protocol (FTP)
- Web-based Distributed Authoring and Versioning (WebDAV)

## Network-Management-Protocols
- Protokolle zur Überwachung und Steuerung von Netzwerkgeräten
- Telnet
- Secure Shell (SSH)
- Simple Network Management Protocol (SNMP)
- Remote Desktop (RDP)

## HTTP
- Hyper Text Transfer Protocol
- Transfer von Websiten

### Aufbau
![[CleanShot 2022-08-08 at 20.45.17.png]]

### Status Codes
- Level 200 (Success)
	- 200: OK
	- 201: Created
	- 203: Non-Authoritative Information
	- 204: No Content
- Level 400
	- 400: Bad Request
	- 401: Unauthorized
	- 403: Forbidden
	- 404: Not found
	- 409: Conflict
- Level 500
	- 500: Internal Server Error
	- 501: Not implemented
	- 502: Bad Gateway
	- 503: Service Unavailable
	- 504: Gateway Timeout
	- 599: Network timeout

## SMTP
- Simple Mail Transfer Protocol
- Austausch von E-Mails
- Kein standarmässiger Schutz

## #TLS
- Transport Layer Security
- Verschlüsselungsstandard bei Datenübertragung
- OSI Layer 5
- Integrity and Confidentiality (CIA-Triad)
- Nur Version TLS 1.2 / 1.3 Sicher
	- Tiefere Versionen können als Sicherheitslücke bewertet werden

### Schlüssel
- Verwendet Schlüsselaustausch-Protokoll
	- #RSA (Nur öffentliche Schlüssel austauschen)
	- #RSA = Asymmetrischer Algorithmus

### Cipher-Suite
- Bestimmt Paramter der Sitzung
- Asymmetrische Verschlüsselung für Verbindungsaufbau (Private Key / Public Key Verschlüsselung)
- Symmetrische Verschlüsselung für Traffic
- Mögliche Probleme:
	- Ungültige Zertifikate
	- Unsichere Cipher-Suite (zum Beispiel MD5)
- Protokolle welche TLS verwenden:
	- FTPS
	- LDAPS
	- SIPS
	- HTTPS
	- SMTPS

### #TLS-Handshake
- Kurzfassung:
	1. Client / Server einigen sich auf Verschlüsselung
	2. Client verifiziert Identität
		- #Chain-of-Trust  / CA
	3. Asymmetrische Kryptographie
		- Schlüsselaustausch für Verbindungsaufbau
	4. Symmetrische Kryptographie
		- Schlüssel für Verbindung verwenden

- Genauere Beschreibung
	1. Aushandeln eines gemeinsamen Schlüssels (Protokoll zur Aushandlung und festlegen des gemeinsamen Schlüssels (DH oder RSA)
	2. Authentisierung der Gegenstelle (Server auf jeden Fall, Client optional (mutual auth)) (RSA)
	3. Aushandeln der Meldungsverschlüsselung (AES, ChaCha20, IDEA, andere) (Warum wird hier nicht RSA verwendet?)
	4. Aushandeln der Meldungsintegrität (SHA, HMAC)

- Ablauf:
```
Client    Server
   --------->     Client Hello (Cipher Suites, Random Number)
   <---------     Server Hello (Cipher Suites, Random Number, Server Certificate, allenfalls Client Zertifikat anfordern)
   --------->     Client Zertifikate, Key Exchange (unterschiedlich, ob RSA / DH)
   <---------     Key Exchange
   --------->     HTTPS Request
   <---------     HTTPS Response
   ...
```

### CA
- Certificate Authority
- Verifiziert Public Key
- Stellt Zertifikate aus
- #Chain-of-Trust für Vertrauenswürdigkeit der Zertifikate

## VPN
- Virtual Private Network
- Virtueller Tunnel zwischen verschiedenen Standorten
- Tunnel ist verschlüsselt

# Netzwerkbegriffe
## Paket
- Geschlossene Dateneinheit
- Beispiel-Paket:
	- Header mit Meta-Daten (Sender, Empfänger, Port, Grösse)
	- Payload
	- Abschluss (Checksum)

## Ports
- Insgesamt 65'536 Ports
- Port 1-1024 "well known Ports"

## Verzeichnisdienst
- Hierarchische DB für Benutzer / Gruppen / Systeme
- Inventar

## #Reverse-Proxy
- Nimmt Requests von Externen Clients an und leitet diese an interne Server weiter

![[CleanShot 2022-08-15 at 19.19.07.png]]

### Ziele
- TLS terminieren
- Lastenverteilung / High Availability
- Caching
- Authentisierung
- API-Gateway
- Sicherheit
	- Firewall (Netz / Anwendung)
	- Malware-Scanner

## #Forward-Proxy
- Nimmt Requests von internen Clients an und leitet diese an externe Server weiter

![[CleanShot 2022-08-15 at 19.22.42.png]]

### Ziele
- TLS aufbrechen
- Ausgehende Angriff detektieren 
	- #ReverseShell
	- #C2

## DMZ
- Demilitarized Zone
- Pufferzone zwischen Internet und internem Netz
- Beinhaltet zum Beispiel: Webserver, Mailserver, Reverse Proxy

![[CleanShot 2022-08-15 at 19.25.43.png]]

### Ziel
- Gegen aussen offene Hosts haben keinen direkten Zugriff auf das interne Netz
- Internes Netz schützen

## Firewall
- OSI Layer 3/4
- Analyisiert IP / TCP / UDP Pakete und entscheidet ob diese durchgelassen werden

### Stateless Firewalls
- Jedes Paket wird "für sich" angeschaut
- Beispiel Webserver:
	- Jede Ausgehende Verbindung erlauben
	- Auf Ports beschränken

### Stateful Firewall
- Firewall merkt sich Zustand der Verbindung
- Komplexer als Stateless
- Beispiel:
	- Ausgehende Verbindung nur auf bereits bestehende erlauben

### Regeln
- DENY / DROP (Paket wird verworfen)
- REJECT (Paket wird verworfen und sender wird das mitgeteilt)
- ALLOW / PASS (Paket wird durchgelassen)
- Regeln erfolgen Top to Bottom (erste Regel welche zutrifft wird angewendet)

### #WAF
- Web Application Firewall
- Spezialisiert für Webanwendungen
- Ziele einer WAF
	- Angriffe detektieren / verhindern
	- Schwachstellen patchen (Virtual Patching)
