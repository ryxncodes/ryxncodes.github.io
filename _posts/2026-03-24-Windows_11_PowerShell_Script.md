---
title: "Building a Windows 11 Readiness Checker in PowerShell"
date: 2026-03-24
categories: [Projects]
tags: [powershell, windows, sysadmin, scripting]
---

I was part of the team running a Windows 11 migration at a medium-sized healthcare organization with over 5,000 endpoints. Only around half of those could be automatically updated, the rest had multiple requirements missing. We kept getting huge lists every week of computers that needed to be worked on and we went through them as fast as we could, but I soon realized there was a lot of repetition. Always having to open the TPM console to check the version, or opening Disk Management to see whether a drive had been converted to GPT or not.

Soon enough I realized this would be a great opportunity to learn PowerShell scripting, so that was my plan.

## Writing the Script

I had never properly scripted in PowerShell before so it was a new one for me. I was able to slowly learn how to query all the relevant attributes, mostly using `Get-CimInstance`. It took roughly a day but eventually I got it working exactly how I wanted. I wrote it on my home computer first and it worked great. I even found out my personal laptop isn't in Secure Boot. I transferred it over to my work computer and it worked perfectly as well, though I did find out my desktop somehow had a Pro license rather than Enterprise.

## Performance on Older Hardware

When testing it out on an older machine, I noticed it took a while, like 30+ seconds to run. I didn't even realize the PC only had 2GB of RAM until the script told me. I did some research and found out about `Start-Job`, which is a great thing. It lets you spin up separate PowerShell instances in the background so multiple queries run at the same time instead of one after another. It can slow down newer computers by a second or two due to the overhead of spinning up those instances, but I figured that was worth it to save 20 seconds on the older ones, which we have a lot more of.

## Adding Drive Detection

Another issue I ran into was that I didn't originally include a drive type checker because I figured we had gotten rid of all the hard drives. Nope. So I added that in. However, when receiving results back from a background job, instead of returning `SSD` or `HDD` it was giving me raw numerical values. Turns out PowerShell serializes objects when passing them out of a job, and enums lose their string names in the process. I had to manually convert the return types to strings inside the job before returning them, and after that it worked fine. It threw me for a loop for a bit though.

## Result

I can call it a success now. I ran it on the slowest PC we had, which still had a hard drive, and it finished in about 10 seconds. Not much longer than it took the batch script just to initialize PowerShell.

The full script is available on my GitHub: [Windows 11 Migration Script](https://github.com/ryxncodes/Windows-11-Migration-Script)