---
title: "AMSI Bypass Notes"
date: "2026-07-21T12:00:00+08:00"
publishDate: "2026-07-20T12:30:00+08:00"
lastmod: "2026-07-20T12:30:00+08:00"
description: "AMSI Notes for myself"
draft: true
tags: ["AMSI", "OSEP", "Reminder", "Notes"]
---
## Executive Summary of AMSI 
AMSI (Antimalware Scan Interface) is a standardized interface that Microsoft **apps** can use to interact with antimalware software in place. 
Applications use many functions, 2 important ones are: `AmsiScanBuffer` and `AmsiScanString` which **scan input for malicious content**. 
Bypass involves *preventing powershell from using `AmsiScanBuffer` and `AmsiScanString`.* Powershell because most windows stuff is in powershell, such as Nishang's entire suite.
The benefit is that malicious actions can be performed much easily, as commands executed do not get scanned.

## Misconceptions
1. Since AMSI is essentially an API, it can be interacted with any AV (ClamAV for example), not just Defender. Though Defender's the main focus of OSEP and is also the most prevalent (Windows Environments are everywhere) and hence although is not the gold standard, is a benchmark. 
2. Bypassing AMSI does not mean that effects will appear. For example, Nishang's `Invoke-mimikatz.ps1` must be bypassed with AMSI bypass techniques, else powershell won't even allow execution. However, because it touches the LSASS process, Defender won't allow it to be executed since the behaviour-cum-payload are detected. But the script will definitely execute, just that it might not fully run. 

## Testing Procedure
Can be tested on native windows OS environment without spinning up a specialised WindowsVM. This is not a good practice, but it's realistically fine since you won't be running anything. With that said, I ran it on my VM.

https://github.com/RythmStick/AMSITrigger/releases/tag/v4

As quoted directly from rhythmstick's [post](https://www.rythmstick.net/posts/amsitrigger/):
>[!quote]
>AMSITrigger will identify all of the malicious strings in a powershell file, by repeatedly making calls to AMSI using AMSIScanBuffer, line by line. On receiving an AMSI_RESULT_DETECTED response code, the line will then be scrutinised to identify the individual triggers.

## Bypass Techniques (Add More)
### Bypass 1: Setting `amsiInitFailed`
This is like the oldest one, and also the first one. If copied off the tweet wholesale, it'll be detected, but this can be circumvented.
The idea is to set the variable `amsiInitFailed` to `true` manually. 

For example:
```powershell
[Ref].Assembly.GetType('System.Management.Automation.Amsi'+'Utils').GetField('amsiInit'+'Failed','NonPublic,Static').SetValue($null,!$false)
```

>[!NOTE]
>The string concatenation is intentional

### Bypass 2: Patching AmsiScanBuffer
[Documentation](https://learn.microsoft.com/en-us/windows/win32/api/amsi/nf-amsi-amsiscanbuffer) states:
>[!quote]
>If this function succeeds, it returns S_OK. Otherwise, it returns an HRESULT error code.

Therefore, the idea is to patch AmsiScanBuffer to always return an error code because via inspection of `amsiUtils` in dnsspy, `AMSI_RESULT_NOT_DETECTED` is returned when there's an error code. 

### Bypass 3: Error Forcing
Either `AmsiUtils.Init` or `AmsiOpenSession` should fail. That's it.


## References and tools (Todo)
Come up with detailed use cases + steps 


1. https://github.com/darkness215/osep-tools/blob/main/amsi-bypass/README.md
2. https://github.com/matro7sh/BypassAV/blob/main/Bypass-AV.md
3. https://github.com/F4l13n5n0w/sn0wldr