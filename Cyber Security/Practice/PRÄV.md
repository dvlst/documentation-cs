# #CTI 
- Cyber Threat Intelligence
- Threat Intelligence ≠ Threat Hunting
- Gathering, Evaluating and Analyzing Data
- Ziel: Strategische Abwehr / Mitigation (Reduizierung) von Schaden
- Details der Bedrohung verstehen
- Auf die wichtigsten und dringensten Gebiete fokusieren
- Wichtige Punkte:
	- Business Continuity nicht stören
	- Vertrauen der Kunden, Partner, Lieferanten sichern
	- Aus der Vergangenheit lernen
	- Ressourcen / Community nutzen
	- Security Fähigkeiten errweitern

![[CleanShot 2022-08-10 at 19.17.43.png]]

### PTI
- Paid Threat Intelligence
- Vorteile:
	- Informationen sind genauer
	- Breite Abdeckung
	- Anforderungen können an Bedürfnisse angepasst werden

## Threat Landscape
- Bedrohung = Jedes Ereignis welches potenziell Schwachstellen ausnutzen kann und so dem Unternehmen schaden kanhn
- Malware Landscape:
	- Interessiert an Informationen
	- Langsam (Viel Vorbereitungszeit)
	- Schwer nachzuvollzuiehen / zu verfolgen

## #EDR
- EDR - Endpoint Detection and Respone
- Monitoring von Endpoints / Geräte von Endusern
- Scanning nach verschiedenen Arten von Malware
- Erkennen von #TTP 
- EDR-Lösungen sind meist proaktiv
- EDR-Lösungen haben meist Real-Time und Historic Views auf die Endsysteme
- Nachteile:
	- Agents müssen auf Jedem Client installiert sein
	- OT (Industrielle Geräte) sind oft nicht supported
	- Externe Geräte sind nicht gut einbindbar

## #XDR
- XDR - Extended Detection and Response
- Monitoring von mehreren Punkten über das gesamte Netzwerk
- Scannet alle relevanten Daten
- Kombination aus #EDR und #NDR

## #NDR
- NDR - Network Detection and Response
- Monitoring des Netzwerks
- Sammelt den Network Traffic und anaylisiert diesen (Verhaltensanalyse, Machine Learning, Artifical Intelligence)
- Erkennen von #TTP mit #MITRE 
- Nachteile:
	- Detaillierte Ansichten über Endpoints sind nicht gegeben

## #CTI Prinzipien 
![[CleanShot 2022-08-10 at 19.38.21.png]]

## #CTI Konsum
- Jedes Unternehmen sollte CTI verwenden
- Grob-Ablauf
1. Alert
2. #IoC Analyse
3. #OSINT - Open-Source Intelligence Analyse
4. #IoC Suche
5. Resolution

## #CTI Types
- Generic Intelligence > Wissen über Geolocation, Applikation etc
- #OSINT > Profis, Malware Sandboxes, Threat Reports
- Human Intelligence > Threat Sharing Groups, Webinars / Seminars
- SOCMIN > Social Network Informations, Media Channels

## #CTI Requirements
- Security Maturity (Eigene Abteilung, Zugeordnete Personen, Spezialisten)
- Methodology (Festegehaltener Prozess)
- Reactive (Firewall / Anti-Virus)
- Proactive (Life-Monitoring > #EDR / #NDR / #XDR, Threat Hunting)

## #CTI Challenges
- Sind wir komprimiert?
- Was ist wichtig / wichtiger?
- Ressourcen vorhanden / nötig?
- Lessons Learned?
- Event Correlation
- Effiziente Analyse

## #CTI Classification
- Unknown - Unknown > Bedrohung ist uns unbekannten und deren Existenz ebenfalls
- Known - Unknown  > Bedrohungen ist uns bekannt aber wir wissen nicht wie sie funktioniert
- Known - Known > Bedrodhung und Funktionsweise sind uns bekannt

## #CTI Gathering and Colleration
- Daten brauchen Kontext
- Korrelation aller Daten in ein einheitliches und lesbares Format

### Daten / Information / Intelligenz
![[CleanShot 2022-08-10 at 19.54.02.png]]

## #CTI Lifestyle
### 1. Direction
- Potential Threats identifizieren
- Prioritäten setzen
- Welche Arte von Quellen und Intelligence werden verwendet?

### 2. Collecting
- Methoden definieren um Informationen zu sammeln
- Internal Sources, Technical Sources, Human Sources
- Metadata, Logs, Forums, Social Media, News etc.

### 3. Processing
- Gesammelte Daten werden zentralisiert ( #SIEM, #EDR und evtl konvertiert)
- Kann mit einem SOAR (Security Orchestration Automation and Response) automatisiert werden

### 4. Analysis
- Aus Daten und Informationen, Intelligenz schaffen
- Zielgruppenorientiert

### 5. Dissemination
- Verbreitung der Information
- Wie oft? Wie dringend?
- Welche Teams brauchen welches Format?

### 6. Feedback
- Kontinuierlicher Prozess um Vorgehen zu verbesseren
- An Zielpublikum ausrichten

## #CTI Intelligence Ebenen
### Strategisch
- Forecast auf bis zu 5 Jahren
- Entscheidung für Tools / Personelle Ressourcen

### Taktisch
- Taktische Informationen
- Verständnis über Verhalten der Angreifer
- False / True Positives unterscheiden
- Rohdaten aus verschiedenen Quellen verbinden können

### Operativ
- Operative Informationen täglich dem Blue Team zur Verfügung stellen
- Informationen über #TTP oder #CVE

### Multiplier
- Schnell umsetzbare Informationen (via verschieden Quellen)
- Intelligenz welche vom Business verstanden wird

## #CTI #Framework
- Vorgehen von Angreifern ist ein komplexer Vorgang in mehrere Schritten
- Wenn man den Vorgang an einer Stelle abwenden kann, kann man den Schaden minimieren
- Beispiel eines Vorgehens eines modernen Angreifers:
	1. Phishing Mail
	2. Client Infiziert
	3. #C2 Channel
	4. #Lateral-Movement 
	5. Server infizieren
	6. Data Theft
	7. Ransomware

### Cyber Kill Chain
- Kette des Angriffs brechen
- Lücken finden und prüfen
- Schritte:
1. Reconnaissence (Social Engineering / Phising)
2. Weaponization (Palyoad)
3. Delivery (USB-Stick / Mail)
4. Epxloit (Payload ausführen)
5. Installation (Malware)
6. #C2 (Command and Controll der System)
7. Actions (lköschen, infiltrieren der Daten / Systeme)

### #MITRE 
- Use Case: Taktiken der Angreifer kennen und erkennen
- Nächste Schritte vorhersehen

### Diamond Modell
- Verfolgt Angreifer über längeren Zeitraum
- Zusatz für Cyber Kill Chain
- Setzt sich zuammen aus
	- Infrastructure
	- Adversary
	- Capabilities
	- Victim

## #CTI generieren
- Personen mit Expertise
- Tiefe Einblicke in Bedrohungen und Rechtliche Lage
- Ziel: Intelligenz später bei Bedrohungen anwenden

## TLP
- Traffic Light Protokoll
- Welche Informationen können geteilt werden
- TLP:RED (Nicht teilen)
- TLP:AMBER (Eigene Organisation)
- TLP:GREEN (Organisation und Partner)
- TLP:WHITE (Öffentlich)

## Use Case
### POP
1.  Security Controls konfigurieren, dass die IOCs überprüft werden.
2.  Signaturen der eingesetzten Tools erkennen.
3.  Phishing Aktivitäten erkennen, falls der Anfreifer IP und Tools wechselt – somit hat der Angreifer keinen leichten Zugang mehr zum / zu dem / den System/en    
4.  ZIEL auf höchster Stufe zu blockieren.
5.  Bei jedem Vorfall den Angriffsversuch analysieren und verstehen.

### Pivoting
- Analyse auf Beweismittel starten
- Indikatoren suchen
- Beispiel:
	1. Trojaner Signatur auf PC gefunnden
	2. Indikatoren auf Threat Intelligence Plattform überprüfen
	3. Weitere Schritte falls Indikatoren vorhanden

## Rekonstruktion
- Late Phase Detection > URL zu Botnet wird erkannt (Phase 5 in Cyber Kill Chain)
- Early Phase Detection > Phishing Mail (Phase 2 in Cyber Kill Chain)

## Threat Modeling
- Entwicklung der Abwehr über Hypothesen
- Informationen über möglichen Angriff sammeln > Hypothese aufstellen

## Pyramid of Pain
![[CleanShot 2022-08-10 at 21.07.32.png]]

## Big Picture
- Viele Elemente spiele zusammen
- Tools müssen dementsprechend korrekt eingesetzt werden

![[CleanShot 2022-08-10 at 20.17.33.png]]

## Brand Intelligence
- Internet nach entsprechenden Marken durchsuchen
	- Ähnliche Domains
	- Hashtags
	- Apps

## Quellen
- Informationen aus offiziellen Quellen beschaffen
	- NCSC
	- [abuse.ch](https://abuse.ch)
	- BSI
	- Gartner Leader
	- Threat Intelligence Partner (SentinelOne)

## Lücken schliessen
- Regelmässig Vulnerability Scans
- Regelmässige Pentest
- KVP > Kontinuierlicher Verbesserungs Prozess
- Automatisierung

# Schwachstellenmanagement
## Zusammenfassung
- Zuverlässige Quelle für Schwachstelleninfos
- Verständnis der Systemlandschaft
- Automatisierung zur Durchsuchung
- Schwachstellen bewerten - #CVSS
- Nicht jede Schwachstelle kann geschlossen werden (Risikomanagement)
- Geschwindigkeit ist essenziell

## Typen
- Software / Hardware Bugs
	- Buffer Overflow
	- Privilege Escalation
- Fehlkonfiguration / Fehlende Sicherheitsmassnahmen
	- TLS nicht konfiguriert
	- Antivirus nicht installiert
- Menschliches Fehlverhalten
	- Mitarbeiter fällt auf Phishing herein
	- Mitarbeiter lässt Angreifer in Gebäude

## Erkennen
### Wie erfährt man über Schwachstellen?
- Security Incident Management
- Periodische Sicherheitstests
- #CTI
- Security Advisories von Herstellern
- Mailling-Listen
- #CVE - Common Vulnerabilities and Exposures and Programm
- CERT-Organisationen
- Gefährdungskataloge
- Herstellerspezifische Schwachstellenfeeds
- #CIS-Benchmarks / Hardening Guides

### Wie erkennt man Schwachstellen?
- #EDR / #XDR / #NDR 
- OpenVAS
- #Nessus
- #metasploit
- Herstellerspezifische Werkzeuge

## Suche
### Was braucht man für proaktive Suche?
- Inventar - #CMDB
	- #CMDB Gap: ungepatcht weil unbekannt
	- Control Scope Gap: ungepatcht weil nicht im Scope
	- Control Gap: ungepatcht weil nicht ganzes Scope abgedeckt
	- Control Quality Gap: ungepatcht weil Patch Mgmt nicht ganz funktioniert
- Verständnis der Systemlandschaft
	- Was ist extern / intern
	- Zugriff User
	- Firewall, Networkhardware, Laufende Services
- Gehärtete Systeme mit Config-Doku (Eingrenzung der Suche)
	- Deaktivierung verwundbarer / unbenutzter Protokolle
	- Aktivierung von Sicherheitsprüfung
	- Aktivierung Zugangskontroll Mechanismen
	- Best Practice: #CIS-Benchmarks
- Automatisierungstool für die Suche

## Detektieren
### Was braucht man für Tools?
1. Schwachstellen-Scanner
	- OpenVAS / Nessus / Tenable / Qualys / Rapid7
	- Vergleichen Software mit Schwachstellen-DB - #CVE 
	- Validieren / Hardening der Systeme
2. Exploit-Frameworks
	- #metasploit, Ironwasp, Pentera, Cymulate
	- Testen von Exploits gegen Systeme
3. Application Security Testen
	- Veracode, Checkmarx, HCL
	- Finden von Schwachstellen in Applikationen (OWASP Top 10)
	- SCA - Software Composition Analysis (Software-Projekte mit Schwachstellen-DB - #CVE vergleichen)
	- SAST / DAST / IAST - Schwachstellen in Sotware-Code / Betrieb finden

### Wie geht man vor?
- Vollautomatisierte Scans
	- Alle relevanten Systeme erfassen
	- Mindestens Vulnerability Scanner
- Pentest
- Red Team Test

## Beurteilen
- Schwachstellen müssen priorisiert werden
- Nicht alle Schwachstellen lassen sich schliessen (Nutzen - Risiko Abwägung)

### #CVSS
- Common Vulnerability Scoring System
- Wichtigste Methode zur Schwachstellenbewertung
- Base Score
	- Ausnutzbarkeit
	- Auswirkung
- Temporal Score
	- Verfügbarkeit von Exploit
	- Verfügbarkeit von Fixes
- Enivronmental Score
	- Anpassung an Firma / lokale Umgebung

![[CleanShot 2022-08-11 at 19.47.36.png]]

# Patchmanagement
## Zusammenfassung
- Gute Metriken - #KRI / #KPI
- Automatisierte Testumgebungen
- Rollouts gut planen / koordinieren
- Container Setups müssen anders behandelt werden als klassische Setups

## Bereitstellen
- Gibt es einen Patch?
- In welcher Form ist der Patch?
- Muss man zusätzliche Massnahmen ergreifen?

## Typen
| Typ  | Reife  | Umfang  | Zweck  |
|---|---|---|---|
| Hotfix  | Instabil  |  Spezifischer Bug |  Workaround / Schnelles beheben  |
|  Patch | (Stabil)  | Spezifischer Bug  | Spezifische Schwachstelle beheben   |
|  Update |  Stabil |  Patches seit letztem Update | Schwachstelle nachhaltig beheben  |
|  Service Pack |  Stabil | Alle Updates einer Periode  | Viele Updates aufeinmal |
|  Upgrade |  Stabil |  Ausstehnde Fixes + Features| Neue Features + Schwachstellenfixes  |

### #Zero-Day
- Responsible Disclosure: Patch-Window bevor Schwachstelle kommuniziert wird
- #Zero-Day Exploit: Exploit Code ohne Responsible Disclosure veröffentlicht
- #Zero-Day Attack: Kriminelle nutzen Schwachstelle vor Bekanntwerden aus

### Alternativen
- Abschaltung der betroffenen Systeme
- Alternativprodukt einsetzen
- Funktionseinschränkung / Work-Around
- Netzwerkisolation der betroffenen Systeme / Services
- Zugangsbeschränkung der betroffenen Systeme / Services
- Virtual Patching (Vorschalten eines Security Gateway bsp. #WAF)

## Testen von Patches
### Wieso testen?
- Updates können zu Fehlfunktion / Schäden führen
- Zeitplan muss validiert werden um Ausfälle zu verhindern
- Rollback Pläne müssen funktionieren / vorhanden sein
- Abhängikeiten berücksichtigen (Wie spielen Systtem zusammen?)
- Updates schliessen Lücken nicht immer komplett

### Umgebung
- Testumgebung sollte Produktivumgebung entsprechen
- Testumgebung solllte von Produktivumgebung getrennt sein

### Vorgehen
- Test-Automatisierung (Rasch ausrollen auf Testsystem)
- Elemente einer Teststrategie
	1. Vollautomatisierte Regressionstests
	2. Vollautomatisiertes Log Monitoring - #SIEM 
	3. Teilautomatisierte Funktionstestst / Business Validierung
	4. Teilautomatisiere Wirksamkeitsprüfung (Exploit Tool / Pentest)
	5. Teilautomatisierter Test-Roll-Out Mechanismum (Rollout sollte getestet werden von Usern)

## Rollout von Patches
### Stakeholder
1. Change Management
	- Überwacht Change-Prozess und erteilt Freigabe
2. Release & Deployment Management
	- Koordiniert Rollout und integriert Patch in Releases
3. Service Asses & Configuration Management
	- Unterhält Inventar / Software Versionen aktuelle halten
4. Service Operations, Service Level Management, Kunden
	- Service-Unterbrüche abstimmen / User vorbereiten
	- Installationsschritte Planen / Service Ops aufbieten
5. CISO, Ops Risk, Risk Owner
	- Risiken bewerten (schnelleren / langsameren Rollout)

### Strategien
- Big Bang
	- Alle Produktiven System auf einmal patchen
- Parallel
	- Parallel ein gepatchtes Produktiv System aufbauen > testen > umschalten
- Sequentiell / Phased
	- Patch auf ein Produktiv System nach dem anderen ausrollen

### Plannung
- Notfallszenarien aufstellen bis Patches ausgerollt werden
	- Monitoring / Threat Hunt
	- Präventive Massnahmen (NIPS - Network Intrusion Prevention / #WAV)
	- Reaktive Massnahmen (Kompromittierte Systeme isolieren, Notfall-Patchplan)
- Grobkonzept / Aufwandschätzung
	1. Risiko-Evaluation erstellen
	2. Ausfallzeiten und Zeitbedarf Grobschätzung
	3. Stakeholder kommunizieren
	4. Roll-Out Strategie
- Ausfallzeiten
	- Wann können welche Systeme ausfallen?
	- Vorbereitung der entsprechenden Systeme (Snapshots / Backups)
	- Rollbacks vorbereiten
	- Wann ist ersonal für Durchführung verfügbar?
- Zeittbedarf
	- Für Dokumentation / Design
	- Für Erwirkung eines Change-Approvals
	- Für Rollout in Testumgebung
	- Für Sicherstellung der Snapshots / Backups / Roll-Back Pläne
- Terminierung und Ankündigung
	- Alle Stakeholder einbeziehen
- Patch Detail-Konzept
	- Rollout Strategie festlegen
	- Testkonzept ausarbeiten
	- Alles testen
	- Roll-Back Konzept ausarbeiten und testen
- Patch Rollout
	- Gemäss Detailkonzept durchführen
	- Validieren / Nach Testing wieder Produktiv schlaten
	- Patch ausrollen
	- Roll-Back Konzept bei Problemen anwenden
	- #CMDB aktualisieren

## Tools für Patching
- Configuration Management Tools (Chef, Puppet, Ansible, SaltStack)
- Deployment Automation Tools (Jenkins, Bamboo)
- Container separat behandeln (Continous Deployment > in Testumgebung > Rollout durch Orchestrator wie Kubernetes)

### Limitationen
- Tools können nur ereichbare Maschinen patchen
- Maschinen müssen in einem definierten Zustand sein

## #CMDB
- Welche Systeme gibt es?
- Welche Softwareversionen sind auf welchen Systemen?
- Welche Abhängigkeiten gibt es?
- Werden alle bekannten Systeme abgedeckt?

### CI
- Configuration Items
- Assets einer Firma
- Server, PCs, Netzwerk, Switches, Firewall, OS, Middleware, DBs, Software, Container, Services
- CIs haben:
	1. Eindeutige ID
	2. Name 
	3. Kurzbeschreibung
	4. Business Owner
	5. Techincal Owner
	6. Asset Klasse
	7. Vendor
	8. Version / Patch-Level
	9. Support Ende
	10. Dependencies
	11. Konfiguration

## Messen
- Mithilfe #KPI und #KRI Performance und Risks bewerten
- #SANS empfiehlt folgende #KPI:
	1. Prozentualle Patch-Abdeckung
	2. Prozentuale kritische Patch-Abdeckung
	3. Prozentuale neute kritische Patch-Abdeckung
	4. Anzahl Systeme mit fehlenden Patches
	5. Anzahl System mit Fehlern nach Patches
	6. Anzahl Applikationen mit Fehlern nach Patches
- Mit folgender #KRI kann man das Risiko bewerten:
	- Wie gross ist die Durchschnittliche Risk-Exposure der letzten 30 Tage?
	- CMDB Abdeckung: Was ist im Inventar?
	- Control Scope Abdeckung: Welche der System sind für Vulnerability Scans vorgehsehen?
	- Control Abdeckung: Welche der Systeme werden vom Scan erreicht
	- Control Quality

## Reporting
- Reporting hilft:
	- Schwächen diagnostizieren
	- Erfolg von Investitionen demonstrieren / Mittel für weitere Investitionen erwerbenden
	- Risiken aus Schwachstellen bewerten

### Wesentliche Reports
1. Control Performance
	- Design Effectiveness - #CMDB Abdeckung / Control Scope / Scope Abdeckung
	- #KRI 
2. Kosten für Schwachstellen- und Patchmanagement Service
3. Patchmanagement Service Performance
	- #KPI 
4. Problemstellen im Patchmanagement
	- #KPI 
	- Systeme mit Fehlern nach Patches
	- Systeme mit fehlenden Patches