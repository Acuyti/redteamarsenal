---
icon: face-viewfinder
---

# Footprinting

### RDP

```bash
# Using NMAP Scripting Engine (detectable by EDR)
nmap -sV -sC 203.0.113.50 -p3389 --script rdp*

# Identify security checks based on handshakes
https://github.com/CiscoCXSecurity/rdp-sec-check
```

### WMI

```bash
# Impacket Script Suite (https://github.com/fortra/impacket)
/opt/scripts/wmiexec.py acu1ty:"SuperStr00ng!"@203.0.113.50 "hostname"
```
