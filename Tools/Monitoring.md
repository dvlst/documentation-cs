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

## [inotify](https://linux.die.net/man/7/inotify)
- Linux Built-in Tool um Dateien / Verzeichnise zu überwachen

## [checkmk](https://docs.checkmk.com/latest/en/intro_setup.html)
- OpenSource Monitoring Tool
- Monitoring von Applikationen / Servern / Netzwerk
- Gratios in RAW Edition

## [Prometheus](https://prometheus.io/) / [Grafana](https://prometheus.io/docs/visualization/grafana/)
- Opensource Monitoring Tool
- Monitoring von Applikationen / Servern / Netzwerk
- Entwickelt für [Kubernetes](https://kubernetes.io/)
	- Container Lösung für Deployment von bspw. Docker-Containern
- Grafana wird als Web-GUI verwendet