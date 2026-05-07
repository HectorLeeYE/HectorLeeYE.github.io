---
title: "Algernon"
date: 2026-04-04
description: "A writeup for Offsec's Proving Ground WriteUp, Algernon"
draft: true
tags: ["OSCP", "CTF", "ctf", "bratarina", "Bratarina", "PgPrac"]
---
## Introduction
Following Lain Kusanagi's list, here's the writeup for Algernon. 

## Enumeration
Given an IP of `192.168.212.65`, the nmap scan shows the following open ports:

|Port|Service|
|-----|-----|
|21|FTP|
|80|HTTP|
|139,445|SMB|
|135||
|5040,7680|???|
|9998|HTTP|

Zoom in on the following:
- Port 21 for anonymous FTP 
- Port 80 for the IIS HTTP site 
- Port 9998 for the HTTP site 
- Port 139, 445 for SMB Enumeration 

![Nmap Scan]()
