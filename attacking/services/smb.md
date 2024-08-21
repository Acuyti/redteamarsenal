---
description: >-
  SMB is a protocol primarily used in Windows environments to provide shared
  access to files and printers over a network. It operates using a client-server
  model, allowing seamless access to remote file
---

# SMB

<mark style="background-color:red;">This chapter is in-progress.</mark>

#### Listing SMB shares

```bash
smbclient -L //203.0.113.50
```

#### Connecting to a SMB share

```bash
smbclient -U acuity //203.0.113.50/smbshare
```
