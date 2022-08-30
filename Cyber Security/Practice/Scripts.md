## base64_encoder
### Requirements
- Braucht eine "b64.txt" 

## Code
```
####################
# import modules
import base64
####################

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


## pcap_anonymizer


## pcap_finder


## port_scanner


## slowloris

## logfile_merging
### About
- Von Hacking-Lab Aufgabe [CSS-05](https://ict-berufsbildung.hacking-lab.com/events/26/challenges/170)
- Merged ein .log-File und ein .json-File in ein neues .json-File welches anaylisiert werden kann

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

### Other Code (not getting it)
```
def process_logs(access_file, forensics_file):
  with open(access_file, 'r') as access_log, open(forensics_file, 'r') as forensics_log:
    forensics = { x['requestId']: x for x in map(json.loads, forensics_log.readlines()) }
    prog = re.compile(r'^(?P<requestId>.*) (?P<remoteAddress>.*) - - \[(?P<timestamp>.*)\] "(?P<verb>[A-Z]+) (?P<url>.*) (?P<version>HTTP/.*)" (?P<status>.*) (?P<responseSize>.*)$')
    for l in access_log:
      try:
        obj = prog.match(l).groupdict()
        obj['timestamp'] = datetime.strptime(obj['timestamp'], '%d/%m/%Y:%H:%M:%S %z').isoformat()
        headers = {}
        req = forensics.get(obj['requestId'])
        if not req:
          print('Could not find request {} in forensics log.'.format(obj['requestId']), file=sys.stderr)
        else:
          for h in filter(lambda x: x != '', req['headers'].split('\n')):
            key, value = h.split(':')
            headers.setdefault(key, []).append(value.strip())
        obj['headers'] = headers
        #write_output_log(obj)
      except Exception as e:
        print("Error {} on line {}".format(e, l), file=sys.stderr)

def write_output_log(obj):
  print(json.dumps(obj))

if __name__ == '__main__':
  parser = argparse.ArgumentParser(description='Process web application log files.')
  parser.add_argument('-a', '--access', help='the acces log file to parse', default='access.log')
  parser.add_argument('-f', '--forensics', help='the forensics log file to parse', default='forensics.json')

  args = parser.parse_args()

  process_logs(args.access, args.forensics)
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