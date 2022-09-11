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
- Unter Wireshark > Preferences > Protocols > TLS > #RSA Keys den entsprechenden Private Key hinzufügen (.pem-File)

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