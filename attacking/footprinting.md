---
icon: face-viewfinder
---

# Footprinting

### DNS

```bash
# Query related nameservers via DIG
dig ns acuity.lab @203.0.113.50

# Query Version details via DIG (for bind servers)
dig CH TXT version.bind 203.0.113.50

# Query all available DNS records via DIG
dig any acuity.lab @203.0.113.50

# Query AXFR Zone Transfer via DIG
dig AXFR acuity.lab @203.0.113.50

# Remember to test Zone Transfer on other DNS zones
dig AXFR internal.acuity.lab @203.0.113.50

# Subdomain Brute Forcing (manual)
for sub in $(cat /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-110000.txt);do dig $sub.acuity.lab @203.0.113.50 | grep -v ';\|SOA' | sed -r '/^\s*$/d' | grep $sub | tee -a subdomains.txt;done

# Subdomain Bruteforce via dnsenum
dnsenum --dnsserver 203.0.113.50 --enum -p 0 -s 0 -o subdomains.txt -f /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-110000.txt acuity.lab
```

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
