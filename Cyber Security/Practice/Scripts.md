# base64_encoder
## Requirements
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

# bruteforce_detector


# keylogger


# pcap_anonymizer


# pcap_finder


# port_scanner


# slowloris


# subdomain_finder
## Requirements
- Braucht eine Domain als Parameter
- Braucht eine "subdomain.txt" mit Beispiel-Subdomains

## Code
```
####################
# import modules
import requests
import sys
####################

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
## Requirements
- Braucht eine [xss_testrings](https://raw.githubusercontent.com/payloadbox/xss-payload-list/master/Intruder/xss-payload-list.txt) file

### Import / Shebang
```
#!/usr/bin/env python3

###########################
# import modules
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