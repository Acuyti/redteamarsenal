# 🔍 Host Discovery

## ICMP

```bash
# Send a single echo request
ping -c 1 199.66.11.4
# Send echo requests to a range
fping -g 199.66.11.0/24
```

## NMAP

{% code overflow="wrap" %}
```bash
# Fast, comprehensive CTF Scan
sudo nmap -sS -sC -sV -T4 -vv -oN nmap_initinal_tcp.txt
# Full sweep for CTF
sudo nmap -sS -sC -sV -T4 -p- -vv -oN nmap_full_tcp.txt
# UDP scan on top 100 ports
sudo nmap 10.129.2.28 -F -sU
# Scanning Top 10 Ports
sudo nmap 10.129.2.28 --top-ports=10 
# Packet trace scan
sudo nmap 10.129.2.28 -p 21 --packet-trace -Pn -n --disable-arp-ping
# TCP connect scan (most accurate - also stealthy)
sudo nmap 10.129.2.28 -p 443 --packet-trace --disable-arp-ping -Pn -n --reason -sT 
# Using Nmap Scripting Engine (NSE) for vulnerability assessment
sudo nmap 10.129.2.28 -p 80 -sV --script vuln 
```
{% endcode %}

## Dnsrecon

<pre class="language-bash"><code class="lang-bash"><strong># Request PTR records of chosen subnet from specified DNS server
</strong><strong>dnsrecon -d acuity.lab -n srvdns01.acuity.lab -r 192.168.1.0/24
</strong></code></pre>
