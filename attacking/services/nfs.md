---
description: >-
  NFS is a protocol commonly used in Unix and Linux systems to enable file
  sharing across a network. It uses a client-server architecture, allowing
  multiple computers to access shared files.
---

# NFS

<mark style="background-color:red;">This chapter is in-progress.</mark>

#### List all available NFS shares

```
showmount -e 203.0.113.50
```

#### Mount an NFS share

```
# Create a directory to serve as a mountpoint
sudo mkdir /var/nfsmountpoint
# Run as root or with sudo privileges
sudo mount -t nfs 203.0.113.50:/ /var/nfsmountpoint
```
