# NFS

Mount an NFS share

```
# Create a directory to serve as a mountpoint
sudo mkdir /var/nfsmountpoint
# Run as root or with sudo privileges
sudo mount -t nfs 203.0.113.5:/ /var/nfsmountpoint
```
