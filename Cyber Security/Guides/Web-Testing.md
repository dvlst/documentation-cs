## Vorgehen bei Web-Testing
1. Active Scan mit OWASP ZAP / Mit Authentication

3. Mit sqlmap nach SQLi suchen
`sqlmap.py -u [POST-GET-URL] --dbs`

3. Session Cookie prüfen
	- In ZAP nach Login das Session Cookie abrufen
	![[CleanShot 2022-09-28 at 09.55.23.png]]
	
	- Prüfen ob Session Cookie einfach verschlüsselt ist ([CyberChef](https://gchq.github.io/CyberChef/#recipe=Magic(3,false,false,'')))
	![[CleanShot 2022-09-28 at 09.59.14.png]]
	
	- Wenn Session Cookie entschlüsselbar versuchen admin Flag zu setzen
	![[CleanShot 2022-09-28 at 10.03.13.png]]
	
	- Session Cookie über Browser Console eingeben und Seite	`document.cookie="_sess=eyJ1c2VybmFtZSI6ImxlZXRoYWNrZXIiLCJhZG1pbiI6MX0="`

4. Mit dirbuster Website auf versteckte Verzeichnise Scannen 
	`dirb [URL]`

5. Nach XSS-Schwachstellen suchen
	- Manuelle Injection mit `<script>alert("XSS");</script>`
	- Automatisierte Injection mit [traxss](https://www.geeksforgeeks.org/traxss-automated-xss-vulnerability-scanner/)
	`python3 traxss.py`