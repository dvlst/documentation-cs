# Cyber Crisis Mangament
## Mitigate Vulnerability
- Welche Sicherheitslücke muss zuerst gepatched werden?

## Vulnerabilty Management Process
- Finding Gaps
	- Scope > Identify > Scan
- Fixing Gaps
	- Validate > Prioritize > Remediate > Rescan > Close

##  #CVSS 
- Common Vulnerability Scoring System
- Industrie Standard für Bewertung der Schwere einer Sicherheitslücke
- Bewertung zwischen 1-10 anhand von verschiedenen Metriken

### Base Score
- Atack Vector = Wo findet der Angriff statt?
- Attack Complexity = Wie komplex ist der Angriff?
- Privilges Required = Welche Berechtigungsstufe muss vorhanden sein?
- User Interaction = Benötigt es Benutzerinteraktion?
- Scope = Sind andere Komponenten betroffen?
- Confidentiality = Wie vertraulich ist der Vorfall?
- Integrity = Wie vertrauenswürdig ist die Informationsquelle?
- Availability = Ist das betroffene System noch verfügbar?

## Validating Vulnerabilities
- False positive: Alarmierung obwohl keine Bedrohung
- Flase Negative: Keine Alarmierung trotz Bedrohung
- True Positive: Alarmierung wegen einer Bedrohung

# Cyber Crisis Response
## #GRC
- Governance, Risk and Compliance
- Governance: Sicherheitskontrollen funktionieren
	- Sicherheitsstrategie an Business Strategie angleichen
	- Informationssicherheitsrichtlinie erstellen und verwalten
- Risk: Sicherheitsrisiken messen
	- Bedrohunge idenitifizieren
	- Reporting / Risiken minimieren
- Compliance: Beachtung der Sicherheitsverpflichtungen
	- Verpflichtungen identifizieren
- Beschreibung von Strategien, Prozessen, Richtlinien das Unternehmen helfen soll Risiken zu identifizieren und minimieren
- GRC tauscht sich mit der Operational Security aus

## SPoF
- Single Point of Failure
- Jeder nicht redundante Part eines Systems welcher den Ausfall des gesamten Systems auslösen kann
- Beheben: Nicht-Redundante Systeme finden und Redundanz abwägen

## Krisenbewältigungsprozess
- Schnelligkeit vor Vollständigkeit

![[CleanShot 2022-08-17 at 21.01.21.png]]

### Initialisierung
1. Lage festellen
2. Stakeholder ermitteln (Wer ist betroffen?)
	- Externe Stakeholder (Kunden, Partner, Gewerkschaften, Politik)
	- Interne Stakeholder (Aufsichtsrat, GL, Mitarbeiter, )
3. Worst Case (für Stakeholder) antizipieren
4. Ziele definieren

- Hilfsmittel:
	- Checkliste mit W-Fragen
		- Was ist passiert?
		- Welche IT-Systeme sind betroffen?
		- Welche Schutzziele sind gefährdet?
		- Wann ist es passiert?
		- Wer ist davon betroffen?
	- Zeitkritische Prozesse und notfall-relevante IT-Anwendungen auflisten
	- Stakeholdermap mit Erwartungen
	- Meldepflichten festhalten
	- Kristenstabprotokoll

### Lagebewertung
- Wo stehen wir mit Blick auf Ziele / Worst-Case-Szenario / Stakeholder?
- Wo haben wir den grössten Handlungsbedarf?
- Was hat sich ereignet? Was wissen wir? Was vermuten wir?
- Welche Informationen wurde bestätigt / wiederlegt?
- Welche Aufträge wurden erledigt?
- Wo stehen wir im Bezug auf gesetzte Ziele?
- Kriterien für Not- / Krisenfälle
	- Gefährdung von Leib und Leben
	- Signifikanter Verstoss gegen Vertraulichkeit / Integrität / Verfügbarkeit / Authentizität
	- Unterbrechung zentraller Geschäftsprozeese
	- Gefahr für Reputation der Organisation
- Leitfrage für Krisenstab?
	- Wurde ein Zeitlimit für die Zieldefinierung gesetzt?
	- Welche Trigger lösen Worst-Case Szenarien aus?
	- Welche Stakeholdererwatungen dienen uns als Richtungslinie?
