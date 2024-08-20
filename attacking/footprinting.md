---
icon: face-viewfinder
---

# Footprinting

### RDP

```
# Using NMAP Scripting Engine (detectable by EDR)
nmap -sV -sC 10.129.201.248 -p3389 --script rdp*

# Identify security checks based on handshakes
https://github.com/CiscoCXSecurity/rdp-sec-check
```
