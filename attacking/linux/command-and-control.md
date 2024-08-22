---
description: >-
  Command and Control consists of techniques that adversaries may use to
  communicate with systems under their control within a victim network.
---

# Command and Control

<mark style="background-color:red;">This chapter is in-progress.</mark>

<mark style="color:blue;">Check the index on the right to navigate this page more easily.</mark>

## Havoc

{% hint style="info" %}
Havoc is a modern, malleable post-exploitation command and control framework made for penetration testers, red teams, and blue teams.\
It's free and [open source on github](https://github.com/HavocFramework/Havoc) written and maintained by [Paul Ungur (C5pider)](https://twitter.com/C5pider)
{% endhint %}

#### Starting the Teamserver

```bash
./havoc server --profile profiles/havoc.yaotl
```

#### Starting the Client

```
./havoc client
```

#### Demon Commands <a href="#id-487f7b22f6" id="id-487f7b22f6"></a>

<table><thead><tr><th width="191">Command</th><th width="195">Type</th><th>Description</th></tr></thead><tbody><tr><td>help</td><td>Command</td><td>Shows help message of specified command</td></tr><tr><td>sleep</td><td>Command</td><td>sets the delay to sleep</td></tr><tr><td>checkin</td><td>Command</td><td>request a checkin request</td></tr><tr><td>job</td><td>Module</td><td>job manager</td></tr><tr><td>task</td><td>Module</td><td>task manager</td></tr><tr><td>proc</td><td>Module</td><td>process enumeration and management</td></tr><tr><td>transfer</td><td>Command</td><td>download transfer module</td></tr><tr><td>dir</td><td>Command</td><td>list specified directory</td></tr><tr><td>download</td><td>Command</td><td>downloads a specified file</td></tr><tr><td>upload</td><td>Command</td><td>uploads a specified file</td></tr><tr><td>cd</td><td>Command</td><td>change to specified directory</td></tr><tr><td>cp</td><td>Command</td><td>copy file from one location to another</td></tr><tr><td>remove</td><td>Command</td><td>remove file or directory</td></tr><tr><td>mkdir</td><td>Command</td><td>create new directory</td></tr><tr><td>pwd</td><td>Command</td><td>get current directory</td></tr><tr><td>cat</td><td>Command</td><td>display content of the specified file</td></tr><tr><td>screenshot</td><td>Command</td><td>takes a screenshot</td></tr><tr><td>shell</td><td>Command</td><td>executes cmd.exe commands and gets the output</td></tr><tr><td>powershell</td><td>Command</td><td>executes powershell.exe commands and gets the output</td></tr><tr><td>inline-execute</td><td>Command</td><td>executes an object file</td></tr><tr><td>shellcode</td><td>Module</td><td>shellcode injection techniques</td></tr><tr><td>dll</td><td>Module</td><td>dll spawn and injection modules</td></tr><tr><td>exit</td><td>Command</td><td>cleanup and exit</td></tr><tr><td>token</td><td>Module</td><td>token manipulation and impersonation</td></tr><tr><td>dotnet</td><td>Module</td><td>execute and manage dotnet assemblies</td></tr><tr><td>net</td><td>Module</td><td>network and host enumeration module</td></tr><tr><td>config</td><td>Module</td><td>configure the behaviour of the demon session</td></tr><tr><td>pivot</td><td>Module</td><td>pivoting module</td></tr><tr><td>rportfwd</td><td>Module</td><td>reverse port forwarding</td></tr><tr><td>socks</td><td>Module</td><td>socks4a proxy</td></tr></tbody></table>
