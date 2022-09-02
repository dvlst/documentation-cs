## base64_encoder
### Requirements
- Braucht eine "b64.txt" 

## Code
### Import / Shebang
```
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

## pcap_decoder


## pcap_anonymizer


## pcap_finder


## port_scanner


## slowloris


## logfile_merging
### About
- Von Hacking-Lab Aufgabe [CSS-05](https://ict-berufsbildung.hacking-lab.com/events/26/challenges/170)
- Merged Einträge eines eines .log-Files und eines .json-Files damit es analysiert werden kann

### Requirements
- Braucht ein log-file und ein .json file

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
#  print(json.dumps(obj))
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

# xss_scanner
### Requirements
- Braucht eine [xss_testrings](https://raw.githubusercontent.com/payloadbox/xss-payload-list/master/Intruder/xss-payload-list.txt) file

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