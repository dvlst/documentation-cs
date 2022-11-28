# Kosten
- Allgemeiner Ablauf der Kosten eines Projekts / Produkt / Software:
![[CleanShot 2022-07-20 at 19.42.46.png]]

### Zweck eines IT-Projekts
- Wertgenerierung (Konsolidierungsprojekt, CRM) > Kosten / Nutzen Vergleich
- Wertsicherung (Buchhaltungssystem, Monitoring-Lösung) > Kostenvergleich

### Investitionskosten
- Kosten währen Projektphase
- Fallen einmalig an
- Externe und Internet Kosten
- Sachbezogene Investitionskosten
	- Consulting
	- Soft- und Hardwareanpassungen
	- Externe Mitarbeiter
	- Implementierung
- Personenbezogene Investitionskosten
	- Personalvermittlung
	- Bonuszahlungen für Mitarbeiter
	- Abfindungen

### Betriebskosten
- Kosten während der Betriebsphase
- Laufende Kosten > Fallen Mehrmals an
- Externe und Interne Kosten
- Applikationskosten
	- Administration
	- Monitoring
	- User-Support
	- Updates
- Plattformkosten
	- Rechenleistung
	- Datenspeicherung
	- Backup
- Allgemeine Kosten
	- Löhne
	- Miete

### Umlaufvermögen
- Lagerkosten (Wieviel Material hat man an Lager?)
- Forderungen von Lieferanten

### Externe Kosten
- Erfolgswirksame Kosten > werden nicht abgeschrieben (Aufwand an Kreditoren)
- Bilanzwirksame Kosten > werden abgeschrieben (Kreditoren an Bank)
- Beispiele:
	- Dienstleistungen
	- Hardware / Software
	- Dateneinkauf
	- Reisekosten
- Kosten für Diensteleistungen
- Kosten für Anschaffungen

### Interne Kosten
- Intern verrechnete Leistungen
	- Internen Leistungen welche zb. ein Projekt in Anspruch nimmt
- Beispiele:
	- Personalkosten (Primärkosten)
		- Löhne, Schulungen
	- Personalkosten (Sekundärkosten)
		- IT-Umlagen (Infrastrukutr, Peripherie, PC / Laptop)
		- Arbeitsplatzbezogene Umlagen (Büroeinrichtung)
	- Infrastrukturkosten
		- Raumkosten (Meetingräume)

## Kostenrechnungen
- Kostenartenrechnung: Welche Kosten fallen an?
- Kostenstellenrechnung: Wo fallen die Kosten an?
- Kostenträgerrechnung: Wofür fallen die Kosten an?

### Aufgliederung der Gesamtkosten
![[CleanShot 2022-07-25 at 21.09.32.png]]

### Schema der Kostenrechnung
- Kostenarten
	- Einzelkosten / Direkte Kosten
		- Können einem Kostenträger (Produkt) zugeordnet werden
		- Sind eher variabel
	- Gemeinkosten / Indirekte Kosten
		- Werden mit einem Umlageschlüssel (Grösseneinheit) auf eine Vorkostenstelle und Hauptkostenstelle umgelagert
		- Kostenstellen = Organisationseinheiten / Abteilungen
		- Sind eher fix
- Variable Kosten
	- Verändern sich mit dem Absatz
- Fixe Kosten
	- Bleiben unabhängig vom Absatz gleich
- Teilkostenrechnung
	- Nur direkte Kosten zugeteilt
	- Gefahr des Vergessens der Gemeinkosten
- Vollkostenrechnung
	- Sämtliche Kosten werden berücksichtigt
	- Komplexer durch Verteilungsschlüssel
	- Unterteilung in IST-Vollkosten, Plan-Vollkosten

### Betriebsabrechnungsbogen
- Darstellung der einzelnen Kosten
![[CleanShot 2022-07-25 at 21.19.08.png]]

## Aufwandsberechnung
- Bei Projekten muss der Aufwand geschätzt werden
- Mit Aufwandschätzmethoden kann dies gemacht werden
![[CleanShot 2022-07-20 at 20.37.09.png]]

- Ablauf der Kostenbeeinflussbarkeit im #Wasserfallmodell
![[CleanShot 2022-07-20 at 20.50.08.png]]

###  Break-Even-Point (BEP)
- Gesamterlös = Gesamtkosten
- Übergang von Verlustzone in Gewinnzone
- Gewinn = 0
- BEP = Fixkosten / (Verkaufspreis - Variable Stückkosten)

### Total Cost of Ownership (TCO)
- Gesamtkosten einer Lösung über Gesamte Lebensdauer
- Lebenszeitkosten
- Direkte Kosten = Einzelkosten = Budgetierte Kosten (TCO-Konzept)
- Indirekte Kosten = Gemeinkosten = Unbudgetierte Kosten (TCO-Konzept)

# Agile ICT-Vorhaben
### #SCRUM
- Entwicklet für Effektiveres Zusammenarbeiten von Produktteams
- Simples Framework
- Schwerpunkt liegt auf Zusammenarbeit & Selbstmanagement
- Zeitpläne werden in kurze Events "Sprints" aufgeteilt

### Agiler Festpreisvertrag
- Fixer Kostenrahmen
- Keine finale Leistungsbeschreibung zu Projektbeginn
- Variable Scope > Change for Free
- Kooperation von Lieferant und Kunde
- Gemeinsame Aufwandschätzung
- Scope-Governance

- Kernelemente:
	1. Definition des Vertragsgegenstandes
	2. Detalspezifikationen von User Stories
	3. Workshop zum Gesamtscope
	4. Riskshare, Checkpoint-Phase und Ausstiegspunkte
	5. Vereinbarung zur Scope-Governance
	6. Festlegen des Bonssystems

- Grob-Vorgehen:
	1. Grobkonzept
	2. Aufwandschätzung
	3. Abschluss Rahmenvertrag
	4. Erste Sprints
	5. Bestimmung der Velocity / Aktualisierung Aufwandschätzung
		- Je nach Korrekheit der Einschätzung wird Aufwandschätzung anders verteilt
		- Wenn höher als geschätzt aufgrund Changes ausser Scope trägt Leistungsbezüger den Mehraufwand
		- Wenn höher als geschätzt und Kompensation Möglich wird der Mehraufwand aufgeteil (aufgrund Riskshare)
		- Wenn höher als geschätzt und Kompensation nicht möglich wird der Festpreis vergütet
		- Wenn wie geschätzt wird der Festpreis vergütet
		- Wenn tiefer als geschätzt werden die Einsparungen aufgeteilt (aufgrund Riskshare)
	6. Vereinbarung Festpreis
	7. Letzte Sprints

### User Story
- Anforderungen an System aufgrund eines Userberichtes

### Story-Points
- Virtuelles das Aufgrund des Aufwand der Anforderung der Referenz-Userstory basiert
- Aufwand der Referenz-Userstory wird als 1 Story-Point gesetzt
- Aufwand kann mithilfe von Story Points oder mit Stunden geschätzt werden
	- Vorteile Story-Points:
		- Relatives Schätzen einfach
		- Sind Teamfähiger
		- Geben Verständnis über Team
	- Nachteile Story-Points:
		- Schwierig zu erklären
		- Abstrakt
	- Vorteile Stunden:
		- Geignet für kleine Storys
		- Einfacher Anwendbar bei internen Projekten
	- Nachteile
		- Detailliertes Controlling / Team weniger gut geschützt
		- Zeigt Scheinwahrheit (Schätzungen ungenau)

# Budgetierung
- Budget liefert finanziellen Rahmen
- "Wieviel Geld hat jemand in einer gewissen Zeit für einen gewissen Zweck zur Verüfgung"
- Zahlen von Budgetierung werden in einem Unternehmen geplant
![[CleanShot 2022-07-20 at 19.20.27 1.png]]

### Budgetierungsrichtlinien
- Vollständigkeit
- Einheitlichkeit
- Zentralisation
- Transparenz / Nachvollziehbarkeit
- Exaktheit
- Aussagekraft
- Periodizitätsabgrenzung
- Wirtschaftlichkeit

## Budgetierungsarten
### Top-Down
- Autoritär
- Vom Umsatz des Gesamtunternehmens runtergerechnet auf den einzelnen Vertriebsmitarbeiter
- Vorteil: Ziele werden konsequent umgesetzt
- Nachteil: Leistungspotentiale werden nicht ganz berücksichtigt

### Bottom-Up
- Partizipativ
- Vom Umsatz des Vertriebsmitarbeiters zum Umsatz des Gesamtunternehmens hochgerechnet
- Vorteil: Eigene Budgetvorstellungen können eingebracht werden
- Nachteil: Bugdetvorstellungen oft nicht mit Zielen von Unternehmen konform

### Gegenstromverfahren
- Vereinheitlichung von Top-Down und Bottom-Up
- Zahlen zuerst von Oben Nach Unten
- Unten wird Gegengeprüft ob Zahlen realistisch sind

### Fortschreibung
- Zahlen vom Vorjahr mit gewissen Anstieg wiederverwenden

### #Zero-Based-Budgeting
- Alles vom Vorjahr verwerfen und immer von 0 afangen

## #Beyond-Budgeting
- Auf Budgetierung komplett verzichten
- Flexible Management-Prozesse
- Radikale Dezentralisierung (aka #Holocracy)

### Vorteile
- Leistung wird nicht anhand von Zielen bewertet / belohnt
- Vergütung dient nicht Verhaltensbeeinflussung, sondern Erfolsgbeteiligung im Nachhinein
- Anreizen zum Eingehen von Risiken
- Kontinuierliche Massnahmenplanung
- Zugriff auf Ressourcen ohne an vielen Stellen nachzufragen

### Gestaltungsprinzipien für ein #Beyond-Budgeting:
- Anforderungen aus dem Unternehmensumfeld:
	- Investoren wollen mehr Leistung
	- Wachsende Innovationsrate
	- Globaler Wettbewerbsdruck
- Erfolgsfaktoren:
	- Schnellere Reaktionsfähigkeit
	- Kontinuierliche Innovation
	- Kundenorientierung
- Managementprozesse sind flexibel
	1. Zielsetzung ist ambitioniert
	2. Bewertung ist im Nachhinein möglich
	3. Kontinuierliche Massnahmenplanung
	4. Ressourcenmanagement ist bedarfsbetrieben
	5. Koordination ist dynamisch
	6. Leistungsmessung kann vielseitig / vielschichtig erfolgen
- Organisation ist dezentralisiert
	1. Selbsteuerung (Wettbewerb mit Klaren Regeln)
	2. Wettbewerbsorientierung
	3. Ergebnisverantwortung an marktnahe Teams
	4. Organisationsformen (Netzwerk kundenorientierter Teams)
	5. Empowerment (Eigenständiges handeln Verantwortlicher)
	6. Transparenz auf allen Ebenen

## Ablauf Budgetierung
![[CleanShot 2022-07-20 at 19.29.25.png]]

## Einflussfaktoren
- Kunden
- Unternehmensvorgaben
- Umwelt-Rahmenbedienungen (Ökologie, Konkurrenz, Gesetze etc.)
- Verfügbare Ressourcen (Know-How, Personal, Infrastruktur)

## Kritipunkte
- Budget kann schon kurz nach Verabschiedung veraltet sein
- Starre Fixierung auf Geschäftsperiode
- Planerfüllung statt Marktorientierung
- Aufwändige und lange Abstimmungsprozesse / Viel Personalressourcen

## Vorteile
- Zwingt zu einer IST-Analyse / Vorrausschau / SOLL-Analyse
- Zwingt über Ressourcen-Management nachzudenken
- Überprüfbare Ziele durch Zahlen
- Bessere Kommunikation, da Begriffe klar definiert werden

## Nachteile
- Budget wird als Statussymbol gesehen
- Grosse Puffer werden eingebaut welche sich kumulieren
- Controller verstehen zu wenig vom Tagesgeschäft
- Fehlendes Commitment des Budgetverantwortlichen
- Ziele festgelegt, keine Massnahmen
- Kein lernen aus der Vergangenheit

## Anforderungen
- Budgets sollen motivieren
- Budgets sollen klar und exakt formuliert sein 
- Budget soll die Flexibilität im Unternehmen nicht einschränken 
- Das Budget sollte zeitlich abgestimmt sein 
- Das Budget soll zukunftsbezogen sein

### Kostenorientierter Ansatz
- Senkung der Kosten

### Leistungsorientierter Ansatz
- Erhöhung der Leistungfähigkeit

## Durchführung der Budgetierung
1. Budgetrunden
	- Vorgaben / Stufengerechtes Herunterbrechen
2. Budgetverhandlungen
	- Iteratives Vorgehen
3. Budget-Sparrunden
	- evtl. #Zero-Based-Budgeting
4. Wo und wie soll gespart werden?
	- Nicht falsch sparen (Ausbildung / Ferien)
5. Best Practice

## Unternehmesbudget planen
1. Unternehmen sollte Engpassfaktoren kennen
	- Absatzmarkt (Absatzplanung) > Wieviel möchte ich produzieren / verkaufen?
	- Personal (Personalplanung)
	- Verfügbares Kaptial (Cashflow-Planung)
2. Ressourcenplanung (Welche Ressourcen sind notwendig?)
	- Personal
	- Räume
	- Maschinen
	- Material
3. Finanzplanung (Wieviel Geld hat man zur Verfügung)
	- Reicht das Geld für die Ressourcenplanung?
	- Wird auf Schätzungen / Extrapolation / Marktforschung / Ziele geplant
4. Budgets zusammenfassen

## Budget / Forecast
- Budgetierung = Planung
- Forecast = Wissenstand über aktuelle Geschäftsentwicklung






