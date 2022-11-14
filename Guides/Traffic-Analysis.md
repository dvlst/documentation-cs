## Network Attacks
### DNS Tunnel
- Viele / Lange DNS Requests
- Non-Unicode Characters in Request
- Es wird ein anderer DNS Server als der Lokale DNS Server angefragt
- TXT DNS Anfragen
- Ziel: Diebstahl von Daten

### ARP poisoning / spoofing
- Viele ARP Requests
- Art des Angriffs: Man in the Middle Attacks zwischen Clients und Router
- Capture Filter zum identifizieren:
```
arp.duplicate-address-detected or arp.duplicate-address-frame
```

### ICMP flood
- Viele Ping (ICMP) Requests mit grösseren Packages Sizes ( > 48 bytes)
- Art des Angriffs: DDOS
- Capture Filter zum identifizieren:
```
icmp and data.len > 48
```

### VLAN hoping
- Viele DTP Requests
- Art des Angriffs: Bypassing Network Access Controlls / Andere VLANs erreichen aufgrund Miskonfiguration von manchen Cisco Switches
- Capture Filter zum identifizieren:
```
dtp or vlan.too_many_tags
```

### Unexplained Package loss
- Viele Package Verluste
- Art des Angriffs: Möglicherweise durch DDOS verursacht
- Capture Filter zum identifizieren:
```
tcp.analysis.lost_segment or tcp.analysis.retransmission
```

## Detection / Port Scanning
### ARP Scanning
- Viele ARP Requests auf Broadcast-Adresse (ff:ff:ff:ff:ff:ff)
- Ziel: Erreichbare IP-Adressen im Netzwerk herausfinden
- Capture Filter zum identifizieren: 
```
arp.dst.hw_mac==00:00:00:00:00:00
```

### IP Protocol Scanning
- Viele Ping (ICMP) Requests welche unreachable sind
- Ziel: Herausfinden welche Netzwerk Protokolle unterstützt werden
- Capture Filter zum identifizieren: 
```
icmp.type==3 and icmp.code==2
```

### ICMP ping sweeps
- Viele Ping (ICMP) echo Requests
- Ziel: Erreichbare IP-Adressen im Netzwerk herausfinden
- Capture Filter zum identifizieren: 
```
icmp.type==8 or icmp.type==0
```

### TCP / UDP ping sweeps
- Viele TCP Requests auf Port 7
- Ziel: Erreichbare IP-Adressen im Netzwerk herausfinden
- Capture Filter zum identifizieren von TCP ping sweeps:
```
tcp.dstport==7
```
- Capture Filter zum identifizieren von UDP ping sweeps:
```
udp.dstport==7
```

### TCP Scanning
- Viele TCP Requests (SYN, null, FIN, PUSH, URG)
- Ziel: Firewall penetrieren, Offene Ports finden
- Capture Filter zum identifizieren von SYN scans:
```
tcp.flags.syn==1 and tcp.flags.ack==0 and tcp.window_size <= 1024
```
- Capture Filter zum identifizieren von null scans:
```
tcp.flags==0
```
- Capture Filter zum identifizieren von FIN scans:
```
tcp.flags==0x001
```
- Capture Filter zum identifizieren von Xmas scans:
```
tcp.flags.fin==1 && tcp.flags.push==1 && tcp.flags.urg==1
```

### UDP Port Scanning
- Viele Ping (ICMP) Requests
- Ziel: Offene Ports finden
- Capture Filter zum identifizieren:
```
icmp.type==3 and icmp.code==3
```

## Tipps
### Hinweis auf Base32 Verschlüsselung
- Nur Grossbuchstaben