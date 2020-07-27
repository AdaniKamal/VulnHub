# Me and My Girlfriend: 1

![image](https://user-images.githubusercontent.com/44063862/88540204-1ad97080-d045-11ea-8702-141724783d35.png)

## Link

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




**By _AdaniKamal_**
