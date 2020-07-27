# EnuBox: Mattermost

![image](https://user-images.githubusercontent.com/44063862/88554003-87119f80-d058-11ea-97a3-835ec74cd279.png)

## :link: Link 

[EnuBox: Mattermost](https://www.vulnhub.com/entry/enubox-mattermost,414/)

## Penetration Testing Methodology

**Reconnaissance**
* Netdiscover
* Nmap
* Sparta/Legion

**Enumeration**
* tftp
* ftp

**Exploitation**
* php -S

**Privilege Escalation**
* Reverse Engineer (IDA)
* Decode (Hex)
* ./secret

**Capturing the flag**
* Local.txt

_______________________________________________________________________________________________________

## Walkthrough

```
netdiscover
```

![image](https://user-images.githubusercontent.com/44063862/88555174-06ec3980-d05a-11ea-8caf-01537cfe4c8f.png)

```
nmap <ip>
```

![image](https://user-images.githubusercontent.com/44063862/88555230-1a97a000-d05a-11ea-9ed1-cedd158443e5.png)

From the nmap scanning. I found that 4 port open. Which is
* 21 (ftp)
* 22 (ssh)
* 80 (http)
* 3389 (ms-wbt-server)
* 8065 (Get using sparta)

I also used Sparta (New version Kali, you can found it as Legion)

![image](https://user-images.githubusercontent.com/44063862/88555632-a14c7d00-d05a-11ea-9034-2b29aa243e1a.png)

Hydra (But also from sparta)

![image](https://user-images.githubusercontent.com/44063862/88556368-862e3d00-d05b-11ea-938b-a11a4c98fd8c.png)

What we got:

* Ftp login (Anonymous) 

I then browse to the http://ip

![image](https://user-images.githubusercontent.com/44063862/88554730-7150aa00-d059-11ea-9568-61f77d6f4c2b.png)

But, it shows ACCESS is FORBIDDEN. And, there is also a several information that we can see which is 

* Ubuntu version = Ubuntu 16.04
* Severname = mattermost
* README.md = in directory of comp software

Login FTP, but, I don't get anything :(

![image](https://user-images.githubusercontent.com/44063862/88556801-00f75800-d05c-11ea-915f-2dc962ade43e.png)

But then, I try login via tftp and GET README.md

```
tftp <ip>
```

![image](https://user-images.githubusercontent.com/44063862/88557062-56336980-d05c-11ea-9b9a-0caa2cf9f4a9.png)

Key that wet got: ComplexPassword0! (Admin)

We browse to http://ip:8065. It give us a login form. Where we can use credentials that we found just now.

![image](https://user-images.githubusercontent.com/44063862/88557461-cf32c100-d05c-11ea-9e15-243bb407c995.png)

Browse it around...

![image](https://user-images.githubusercontent.com/44063862/88557574-f4bfca80-d05c-11ea-9c19-01cadff24948.png)

```
http://192.168.235.137:8065/admin_console/plugins/plugin_zoom
```

Set it to true. and browse to the ZOOM URL

![image](https://user-images.githubusercontent.com/44063862/88557705-246ed280-d05d-11ea-86c6-3f06b1f49409.png)

```
http://192.168.235.137/JK94vsNKAns6HBkG/AxRt6LwuA7A6N4gk/index.html
```

![image](https://user-images.githubusercontent.com/44063862/88557847-55e79e00-d05d-11ea-8895-5e104751cef4.png)

Credentials that we got: ftpuser:ftppassword

So, what we waiting for???

```
ftp <ip>
```

![image](https://user-images.githubusercontent.com/44063862/88558125-bbd42580-d05d-11ea-8bb4-117d21743070.png)

![image](https://user-images.githubusercontent.com/44063862/88558399-09e92900-d05e-11ea-9e68-9680d43be5ff.png)

![image](https://user-images.githubusercontent.com/44063862/88558431-17061800-d05e-11ea-928b-70798d266a88.png)

```
cat message
```

![image](https://user-images.githubusercontent.com/44063862/88558462-24bb9d80-d05e-11ea-99ec-a02498bc67e2.png)

What you think is this?? Well, they will not just welcome us. HAhahahaha.. Why don't we try login to SSH? 

```
ssh mattermost@192.168.235.137
```

> Credentials (mattermost:Welcome!!!)

![image](https://user-images.githubusercontent.com/44063862/88558644-66e4df00-d05e-11ea-9e12-1813f4ebb86f.png)

BOOM! Yeahh.

```
cat README.md
```

![image](https://user-images.githubusercontent.com/44063862/88559226-22a60e80-d05f-11ea-9782-e157c1f0aa54.png)

Secret key: 48912

![image](https://user-images.githubusercontent.com/44063862/88559463-6dc02180-d05f-11ea-9b1e-ae1f25d2d33d.png)

OMAIGADD!! It's invalidd

Hosting the file on the server (php server script)

```
php -S 0.0.0.0:8000
```

![image](https://user-images.githubusercontent.com/44063862/88559671-b2e45380-d05f-11ea-8af6-abf56bd8414e.png)

Download onto attacker machine (kali)

![image](https://user-images.githubusercontent.com/44063862/88559871-f939b280-d05f-11ea-8ab4-4e6c2501da64.png)

Try reverse using IDA

![image](https://user-images.githubusercontent.com/44063862/88560014-238b7000-d060-11ea-8eb3-5bca6f182d37.png)

Decode:

[Rapid tables](https://www.rapidtables.com/convert/number/hex-to-decimal.html)

![image](https://user-images.githubusercontent.com/44063862/88560153-59305900-d060-11ea-8d85-3bee9e57536f.png)

We got a new key: 62535

```
./secret
ls
cd /root
cd Desktop
ls
cat local.txt
```

![image](https://user-images.githubusercontent.com/44063862/88560213-6fd6b000-d060-11ea-9021-53c11dc4cb5e.png)

**Local.txt:are2020nehoc0601Great!**

Okay, Thats all for Matermost Box. Thank you for reading. :white_flower:

**By _AdaniKamal_**
