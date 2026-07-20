---
title: "OSCP && Beyond!"
date: "2026-07-20T16:00:00+08:00"
publishDate: "2026-07-20T16:00:00+08:00"
lastmod: "2026-07-20T16:00:00+08:00"
description: "Passing OSCP and Beyond"
draft: false
tags: ["OSCP", "OSEP", "pass", "checklist"]
---
## Summary
This blog post just quickly summarises my experience leading up to and taking the OSCP. More importantly, there's a checklist I made at the end so that you can gauge and check if you're ready for the exam yourself.

## Preparation
The course material (and related expense) I consumed prior to the OSCP certification exam were as follows:

|Item|Cost (Rounded UP)|
|-----|-----|
|The 90 Day course bundle | 2k SGD |
|4 Months Pgprac/PgPlay Access| Roughly 15 * 4 = 60SGD|
|HTB Labs|About 150SGD (Note that I bought this last year during a discount, not specifically for the OSCP, and had a year long sub)|
|THM|About 15sgd * 2 = 30SGD|
|Virtual Hacking Labs|100SGD|
|Lain's List at https://docs.google.com/spreadsheets/d/18weuz_Eeynr6sXFQ87Cd5F0slOj9Z6rt/edit?gid=487240997#gid=487240997| FREE |

This makes the total cost about 2200SGD. I'm happy!
![Robin](./static/robin.gif "**YAY**")

## Reviews of Resources Used
1) Prioritise completion of challenge labs in the OSCP course. In particular, OSCP A,B,C **must** be completed. I personally did all the challenge labs except the very last one, more so due to a lack of time rather than inability to / lack of willigness. 
2) PgPrac was used to brush up on weak concepts, stuff I didn't know etc etc. It's good to do because I managed to firm up my methodology since the exam's a 24h proctored grind, so you need to autopilot more and use your brain less *because more brain usage leads to more stress when stuff doesn't work*. I did all the PgPrac boxes (Linux, Windows, AD).
3) HTB labs was done mostly because I had a prior subscription, so I just did it since more practice never hurt. I did about 20 linux, 20 windows, and 10 AD's just to expose myself to different methods. 
4) THM was used on a whim, more so only because I wanted to just check out the priv esc labs as when I was doing my notes, I didn't really know how to categorise them so I used the linux priv esc and windows priv esc labs to just create sections so I knew what to look out for. Especially with their recent moves to lock stuff behind premium walls whilst not offering professional or quality education (unlike HTB which has moved towards providing quality content), I can't really recommend it. 
5) I really recommend virtual hacking labs. I was exposed to different kernel exploits, reminded of the importance of full enumeration, and mostly helped me concretise everything I knew. It was really realistic. 

## My Exam
I started at 10am Singapore Time. Honestly, I auto-piloted most of the way through. Every 15 minutes I stretched, and everytime I found any flag, I would use the toilet. As a result, I compromised the AD domain within 1.5 hours, and had a meal. After that I did the first standalone in roughly an hour and 30 minutes, took a toilet break, and went for the second standalone. After that I managed to get the first flag of the second machine in an hour, and proceeded to go for a run. I achieved passing marks by about 7pm or so, so I felt quite relaxed. After the exercise, I decided to push for 100 marks, and grinded out the privilege escalation and final standalone to 10pm, went to bed, and continued from about 5.30am to 8.30am. There was a last 20 minue desperate rush since I was bored and whilst sipping my cup of tea, I went to read the OSCP exam guide and found that they wanted examinees to take screenshots of the flags with the IP of the machines, which I spent 20 minutes doing so before finally ending it quite flustered. After I obtained the passing mark, I did the machines whilst watching a combination of Reincarnated as a Slime and The Hobbit.

## Advice
I only have 2 pieces of advice.
1) Practice. Unfortunately since the OSCP is a CTF, practice will make perfect. There's no silver bullet command that will one shot work all the time, but with practice, you build a methodology and develop an instinct on what to look for, and what to ignore. It's good to complete Lain's list, but for me, I consistently did machines beyond Lains List, such as doing the seasonal HTB machines, VulnHub, HackmyVM, extra PgPrac stuff. Not all the machines I did were relevant to the OSCP strictly, but I managed to learn, and firm up my methodology. For instance, in my exam, I consistently ran `nmap -T4 -p- -A -oN nmap1.txt --min-rate 1000` before using the toilet or whilst stretching. I've seen fancy commmands/workflows which suggest using rustscan to identify ports, then enumerating services, versions, vulns, all sequentially. However, because the OSCP is just a CTF, going for a CTF-esque approach doesn't have any repercussions. 

2) Good notes/checklist. Practice will allow you to internalise all these things and make it second hand. For my exam, I only referred to my notes to copy paste the rdp command that creates a shared network drive to the session. Apart from that, the only time I used obsidian was to copy paste findings, and just checking the screenshots folder to ensure that I had taken a good flameshot pic (since my flameshot is a screen cap and not the window which you can resize). Good notes/checklists should tell what to do in what situation, list out all things to try before throwing in the towel. This has to be created as you practice. Your checklist should cover everything you have to do. For example, don't just write "directory brute-force". Write "drectory brute-force all directories manually. Use dirbuster wordlist, and seclists. Use both with and without file extensions if applicable".

## Tools used
Here's a list of tools I used throughout the exam. I really recommend them since I chose these tools for their Quality of Life features.

|Tool Name|Link|Function|
|-----|-----|-----|
|Penelope|https://github.com/brightio/penelope|Auto Upgrade Shell. Allowed me to get a TTY and tab completion because although I know how to upgrade to a TTY, I still use the default `zsh` terminal in Kali which doesn't work well with the `CTRL+Z` trick.|
|Credspray|https://github.com/strikoder/CredSpray|Sprays specified protocols with and without local auth. With this, I confess I didn't bother enumeration of the internal network since all I did was just spray anything and everything with everything I had.|
|Credshunter|https://github.com/NeCr00/Credential-Hunting|A good thing to run first due to it's lightweight nature so all passwords are dumped out immediately, allowing you to quickly strike off checking for creds in your checklist first, and once you exhaust all other options, do it manually yourself. My experience with this is that it does a pretty decent job.|
|BloodyAd|https://seriotonctf.github.io/BloodyAD-Cheatsheet/index.html|Slightly easier than `net` to do LDAP(s) stuff. Fixes commands like `$domain`, `$target` in positions so it's just copy pasting/auto-completion, speeding up workflow. (I also used bloodhound, which should be obvious).|
|Caido|https://www.kali.org/tools/caido/|**Burpsuite CE will work just as well**, but I used caido (and disabled AI automation inside) because Burpsuite's slow on my KaliVM, and caido's much faster. I only swapped to caido like last minute, so burpsuite will work just as well.|
|haiti|https://github.com/noraj/haiti|Allows for identification of hashtypes, skips the step of going to hashcat module page.|

## Checklist
### Must knows
1) nmap Enum fully (dont need any fancy identify port first then check service bla bla, i got away with nmap -T4 -p- -A $target -oN nmap1.txt --min-rate 1000)
2) be able to fingerprint as many ports as possible with both nmap and manually with as specific a tool as possible (eg snmpwalk, telnet)
3) Abuse misconfigured services for anonymous access for ftp, smb, rpc (username enum, files, read write etc)
4) Check for robots.txt, sitemap.xml, well-known.txt/xml, .git, /.git/HEAD`
5) How to dir brute-force with different wordlists + fingerprint what extension to dir brute-force with that 
6) Fingerprint site + identify all important config files
7) Exploit file upload into webshell into RCE  (Double extension, alternative extension, magic bytes, .htaccess attack) 
8) How to hydra anything and everything
9) SQL inject Chain (Either exfil data get creds or get a shell) 
10) Dir traversal Chain (Exfil data get creds from important config file, diff ssh key, determine user to attack) 
11) LFI chain (LFI into RFI into SSRF into important file into fingerprint backend) 
12) Command Inject into RCE 
13) How to use ligolo + how to send a reverse shell through ligolo to kali (its via add_listener btw) + how to comm with local services (else you'll need to port forward)
14) How to chisel (in case, though likely won't happen) 

#### Win Priv Esc
15) how to gen a rev shell .exe, add a user 
16) Identification && exploitation of groups (BackupOps, ServerOps, DnsAdmin, LAPSReader) You need more than 1 way of exploitation
17) Full flow of unquoted service path 
18) reg perms (autorun, alwaysinstallelevated)
19) Insecure exe
20) HOW TO RUNAS (either manually or use runascs.exe)
21) Where passwords are found (panther, powershell hist, etc etc)
22) Identification of non-normal files 
23) Scheduled tasks
24) Startup apps 
25) Running PrivescCheck.ps1, PowerUp.ps1, then WinPEAS
26) SeImpersonate (Usage of Sigma, God and rogue)
27) Other tokens like SeBackup, SeRestore (More than 1 way) 

#### Linux Priv Esc
28) As many ways to get shells as possible (sudoers, passwd, shadow, revshell) 
29) cron jobs (file perm, PATH, wildcard, attack script, attack library, identification) 
30) SUID/SGID (as many of them as possible) 
31)  file with capability (+ep chown etc etc) 
32) fingerprint location of ALL config files, important files  (yes even the webserver)
33) find all passwords 
34) Kernel exploits (know which version of cow, screen, identification of sudo, polkit). Do note the cow part, there's many many types of cows beyond cow1 and cow2 shown in linpeas and they attack different things
35) PE scripts (linux smart enum && linpeas are good enough). Tee everything to a file and check 
36) Port forward

#### AD specific
1) Where to get a nmap binary
2) Where to slam your intial creds (every open port) 
3)  asrep, kerberoast both remotely from kali and local 
4) Grab usernames and prepare to spray (plus pray) 
5) recheck share
6) steal hash with responder (use -A) 
7) pass the hash, pass the password, pass anything etc etc 
8) diff ways to get shells through rpc, smb,winrm,sql,rdp (like rdesktop, alternative to xp_cmd_shell, wmiexec2, smbexec etcetc)
9) dump everything (sys + sam cache, lsa, ntds.dit) + crack
10) bloodhound 

### Good 2 know
1) XSS attacks into RCE 
2) Getting NTLMS for 9,10,11,12
3) Shell escape 
4) WSL attack
5) ADCS (good to practice)
6) very, very, super basic AV evasion

## Conclusion
And that's it! Feel free to ask questions, but I will not reveal any confidential information about the exam!
And once again, if your question is "how to prepare", my answer is- "Just start".

Onwards to the OSEP! 🥲