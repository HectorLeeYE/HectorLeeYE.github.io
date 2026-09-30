---
title: "Sp1derL1lly, The First Update"
date: "2026-09-28T11:00:00+08:00"
publishDate: "2026-09-28T11:00:00+08:00"
description: "A new project- Sp1derL1lly"
draft: true
tags: ["Browser In The Middle", "Redteam", "Phishing"]
--- 

## Background
Traditionally, phishing attempts are conducted by cloning the target's HTML site onto an adversary-controlled domain, which is then deployed. There have always been a couple of issues with past attempts. The main weakness was always that this approach really only worked for Single-Page Applications. **Complex web-apps, or even some dynamic SPAs, with heavy JS and heavy backend queries, appear glitchy when displayed using a static clone, rendering user paths unusable, and overall, lower the effectiveness of the campaign.** This is important from a business-perspective especially because for external consultant red-team engagements, projects are often conducted in phases, rarely in one lump sum. Whilst OSINT and non-invasive reconnaissance will be conducted, the first real "grading" by the client will be project deliverables with real statistical evidence, ergo, the success of the phishing campaign. Although this is less important for internal red-teams, it is still a good deliverable since it reflects quality and quantity of work done, and that nobody is actively sitting on their butts doing nothing. 

## (Other) Weaknesses of Traditional Phishing Campaigns conducted by red-team engagements
|Issue|Current Mitigation or Explanation|
|-----|-----|
|Complex SPA/web apps render improperly on static clone|AI model reiteration can eventually produce a convincing copy given enough time.|
|Complex MFA Handling|On proper engagements, MFA is now a given (mostly it's Microsoft Authenticator). Standard reverse-proxies struggle with this. No good way to mitigate.|
|Scaling + Isolation|Some vigilant employee will report the link, and threat hunters will come to interact with the target, first via automated tools, then via a hands-on. If the underlying infrastructure is exposed, leading to an attack on the red-team itself, resulting in objective failure.|

## Sp1derl1lly
Therefore, I opted for a different approach- Usage of Browser In Browser. 
The red-teamer still has to craft the phishing point of entry: Email, QR Code, Text Message etc. However, when a victim clicks the link, instead of being redirected to a cloned phishing site (which raises suspicion), they visit their legitimate company site, albeit in a browser instance controlled by the red-team. 
Since it's controlled by the red team and is a legitimate site, issues about MFA are a non-concern. The victim will also hardly know the difference, and will be able to peruse their webapp in great detail. Simultaneously, the red-team is able to capture cookies, authentication tokens, see information, and even persist the session when the victim closes the tab (since everyone is guilty of just closing the tab, nobody logs out). As a consequence, the red-team can plan for further attacks, or start planning a more guided terrain study, or even who to spearphish next. 

## Weaknesses of Sp1derl1lly
The main issue with Sp1derl1lly is **latency**. Although I've taken every measure to ensure that the code and deployment is as lean as possible so that the victim does not experience lag/cursor flickering or any other common issues with BIB instances, ultimately, the red team has to deploy the engagement on an aged domain that is close to their targets. Luckily, as red-team engagements typically proceed with authorisation from the CISO, getting permission to provision a domain and piggyback off a company owned domain is an easy, often fulfilled request. 

## Wildcard Factors
One wildcard factor of Sp1derl1lly is the resistance towards threat hunters. In a red team engagement, the objective is to evaluate the defences the company has, and also validate the playbook the blue team has planned/implemented against known threat actors in their industries. Therefore, when an employee reports the phishing email because **eventually, some employee will have clicked it, realised that he or she heavily messed up, wants to not do 100 hours of remedial cybersecurity training or get written up, and immediately reports the email to lessen the impact.** The threat hunters will therefore come knocking on the site.
Via BIB implementation, I'm able to control the requesting IP Geolocation. As a result, I can for example, redirect them to the legitimate site without the BIB instance, or for what I'm currently doing, show them a generic error page. This is stronger because this can be customised, and is easily thrown up. Should the threat hunters then attempt to use a VPN to mimic the target country's IP after some eventual deduction on the factors, they will only be able to gain understanding that a phishing campaign is happening because all instances execute in a Docker container. Although I've done the usual kiosk hardening measures, should they somehow break out, a docker instance is useless. *One planned feature would be a monitored beacon in the container, if the suspiciously named file directory containing it is accessed, a notification is sent to the red team to notify them that a threat hunt has started and defensive measures need to be taken, the phishing campaign needs to step a notch immediately because the campaign's lifespan is nigh, and/or to credit the blue team in an email to the CISO/initial report*.

## Note
Sp1derl1lly does not cover the following 2 things:
1) Delivery mechanism. I will not cover how to write a convincing phishing payload because it's unethical. Go and figure that out yourself.
2) Website exploitation. The red-teamer will have access to the user's cookies and session tokens. However, web app attacks like injection of DOM XSS, SQL injection, exploitation etc is not in the scope of this repository because attacks on infrastructure may not be in scope. The intended path is hijack instance -> Further enumerate/attack/exfiltrate -> Report a win and secure funding + permission for the next contracted step. 

Although I welcome feedback and suggestions, any comments about the above 2 points will be ignored. 

## Warnings
This tool is meant only for red-team, authorised offensive engagement purposes. Although I have no legal sway over you deploying it in a black hat campaign, know that I will be extremely disappointed and will not hesitate to report you to the authorities if I can. 

## When is it coming?
I'm just dotting the I's and crossing the T's, but it should come out by next week. I need to also do some extra tests + record a demo video. 