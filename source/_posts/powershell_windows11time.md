---
title: Time changed due to Linux UTC - how to change it on Windows 11
date: 2025-06-10
cover: /img/powershell_windows11time.png
categories: PowerShell/cmd
tags: powershell, windows11, linux, cmd, terminal, dualboot
---

## Introduction

In this post, I will have a look at how to change to the local timezone, that is set in UTC as default.

## Purpose

The problem I was facing was that my Windows 11 was showing timing 2h before the CEST (Central European Summer Time).

The cause of this was due to the fact that I'm using dual boot on my laptop - I am currently using Windows 11 and Ubuntu 24.04.2 LTS.

To fix this, I had to search online, and ask ChatGPT for some help.

## 1. Run PowerShell (run as Admin) and set registry key

On PowerShell, this can easily be achieved by running this code:

```powershell
New-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\TimeZoneInformation" -Name RealTimeIsUniversal -Value 1 -PropertyType DWord -Force
```

What this essentially does, is setting the registry key in Windows 11 to interpret the hardware clock as **UTC**, just like what Linux does.

## 2. Set timezone to correct timezone

Afterwards, For my case, I had to run the following code for CEST:

```powershell
tzutil /s "W. Europe Standard Time"
```

## 3. Restart your PC

After restarting my PC, this set my Windows time to the fixed timezone as CEST.

![Time to sleep!](powershell_windows11time/powershell_windows11time.png)