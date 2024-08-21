---
description: >-
  SNMP is used for network management, allowing administrators to monitor and
  manage network devices. It operates by exchanging information between network
  devices and a central management system.
---

# SNMP

<mark style="background-color:red;">This chapter is in-progress.</mark>

#### Enumerating community strings with [onesixtyone](https://github.com/trailofbits/onesixtyone)

```bash
onesixtyone -c /opt/useful/SecLists/Discovery/SNMP/snmp.txt <IP>
```

#### Retrieve MIB records with [snmpwalk](https://manpages.debian.org/bookworm/snmp/snmpwalk.1.en.html)

```bash
snmpwalk -v2c -c <community string> <IP>+
```

#### Enumerating [OIDs ](https://www.alvestrand.no/objectid/)for know community strings with [braa](https://github.com/mteg/braa)

```bash
braa <community string>@<IP>:.1.3.6.*

# don't forget to try
braa <community string>@<IP>:.1.3.6.* -2 # claim to be a SNMP2C agent
```
