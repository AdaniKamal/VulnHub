# Me and My Girlfriend: 1

![image](https://user-images.githubusercontent.com/44063862/88540204-1ad97080-d045-11ea-8702-141724783d35.png)

## :link: Link 

[Me and My Girlfriend: 1](https://www.vulnhub.com/entry/me-and-my-girlfriend-1,409/)

## Penetration Testing Methodology

**Reconnaissance**
* Netdiscover
* Nmap
* Sparta/Legion

**Enumeration**

**Exploitation**
* Burp Suite/Extension for browser

**Privilege Escalation**
* sudo php

**Capturing the flag**
* Flag1
* Flag2

_______________________________________________________________________________________________________

## Walkthrough

![image](https://user-images.githubusercontent.com/44063862/88540432-80c5f800-d045-11ea-989f-ef8da66fd016.png)

```
netdiscover
```

![image](https://user-images.githubusercontent.com/44063862/88540459-8f141400-d045-11ea-873d-1fc6818ddbe1.png)

```
nmap 192.168.235.141
```

![image](https://user-images.githubusercontent.com/44063862/88540509-aa7f1f00-d045-11ea-8527-62396bea38bd.png)

From the nmap scanning. I found that 2 port open. Which is
* 22 (ssh) 
* 80 (http)

I also used Sparta (New version Kali, you can found it as Legion)

![image](https://user-images.githubusercontent.com/44063862/88540613-dac6bd80-d045-11ea-915c-a2e04f770880.png)

This is the result from sparta, same as nmap.

I then browse to the http://ip

![image](https://user-images.githubusercontent.com/44063862/88540636-e87c4300-d045-11ea-96e6-90b23560e64c.png)

View page source, will give us some more info

![image](https://user-images.githubusercontent.com/44063862/88540692-ffbb3080-d045-11ea-9095-109adac471d8.png)

**HINT:** X-Forwarded-For: localhost

![image](https://user-images.githubusercontent.com/44063862/88540905-6e988980-d046-11ea-92cb-5636f95af63a.png)

I found that we can do it using Burp Suite.

![image](https://user-images.githubusercontent.com/44063862/88540957-8cfe8500-d046-11ea-9987-b5cfd0fb19a3.png)

View HTML, will give us

![image](https://user-images.githubusercontent.com/44063862/88541060-ba4b3300-d046-11ea-9a75-3076c84c4dea.png)

And!! We can also use extension in browser. 

![image](https://user-images.githubusercontent.com/44063862/88541095-ccc56c80-d046-11ea-8ed6-f7970e570f4b.png)

Okay, now we got the login page. Let's register as user

![image](https://user-images.githubusercontent.com/44063862/88541207-f1b9df80-d046-11ea-8d7d-7406caac40c8.png)

This is the page after register user.

![image](https://user-images.githubusercontent.com/44063862/88541223-faaab100-d046-11ea-92fe-9d11da59f10e.png)

At profile page, we can change the ID. Mine (ID=12), I try to change. Until I found Alice’s

![image](https://user-images.githubusercontent.com/44063862/88541317-22017e00-d047-11ea-84c3-e751846d5335.png)

Just by "View page source" or "Inspect" this page. We can see the password for user Alice.

![image](https://user-images.githubusercontent.com/44063862/88541374-32b1f400-d047-11ea-8402-cea29e1fb52a.png)

Value: alice/4lic3

Okay, now we can try SSH using this credentials that we got.

```
ssh alice@192.168.235.141
```

![image](https://user-images.githubusercontent.com/44063862/88541773-e7e4ac00-d047-11ea-9ddc-94169be02a84.png)

```
ls -al
cd .my_secret/
ls -al
cat flag1.txt
```

> **Flag1: gfriEND{2f5f21b2af1b8c3e227bcf35544f8f09}**

```
cat my_notes.txt
```

![image](https://user-images.githubusercontent.com/44063862/88541938-25493980-d048-11ea-8cf1-5c5795dd3b59.png)

```
sudo -l
```

> For Privilege Escalation

![image](https://user-images.githubusercontent.com/44063862/88542021-54f84180-d048-11ea-97fc-7ab2a81ac7b0.png)

As usual, we will refer tu [GTFObins](https://gtfobins.github.io/gtfobins/php/)

![image](https://user-images.githubusercontent.com/44063862/88542091-73f6d380-d048-11ea-87d1-31e0f0eb5466.png)

```
cp /etc/passwd .
```

![image](https://user-images.githubusercontent.com/44063862/88542589-39da0180-d049-11ea-860d-563cc06f32e2.png)

```
sudo php -r 'rename("passwd","/etc/passwd");'
```

```
su -
```

![image](https://user-images.githubusercontent.com/44063862/88542678-6261fb80-d049-11ea-88c6-ea8bb2646bce.png)

BOOM!! root and straight away flag. :)

![image](https://user-images.githubusercontent.com/44063862/88542718-74439e80-d049-11ea-9b82-40ae4705c179.png)

> **Flag2.txt: gfriEND{56fbeef560930e77ff984b644fde66e7}**

Okay, Thats all for Bob and Alice. Thank you for reading. :white_flower:

**By _AdaniKamal_**
