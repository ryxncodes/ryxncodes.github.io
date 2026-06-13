---
title: "Analyzing a Suspicious Windows Service From a Paid Game Utility"
date: 2026-06-12
permalink: /posts/analyzing-a-suspicious-windows-service/
categories: [Projects, Security]
tags: [malware-analysis, windows, cybersecurity, static-analysis, ai]
---

I recently got pulled into a small malware analysis rabbit hole after a friend asked me to independently investigate concerns about a paid game utility shared through a Discord community. They thought it might be something I would be interested in looking at, and they were right.

The program came from an unknown third-party developer, so I wanted to take a closer look at what it installed and how it behaved.

The context I was given was that the app was tied to paying customers, and the website used Discord account information and hardware identifiers to handle subscriptions, product access, and account sharing prevention. That part alone did not immediately seem crazy to me. A paid app using Discord identity, HWID checks, and entitlement logic is not automatically malicious. Annoying maybe, but not surprising.

The part that stood out was the installed Windows service.

The artifacts I reviewed showed that the program installed a persistent Windows service named `PSDeviceDiagnosticsHost`, with the display name `Microsoft PowerShell Diagnostics Device Host`. It was placed under a PowerShell diagnostics-themed path and configured to start automatically as `LocalSystem`.

That is where the licensing explanation starts to become a lot harder to accept.

## My background going into this

I want to be clear about my experience level here. I am not a professional malware analyst, and I am not going to pretend I manually reverse engineered the whole thing from scratch.

I have been learning basic malware analysis through TryHackMe, cybersecurity labs, and self-study. I understand some of the core ideas, including static and dynamic analysis, suspicious persistence, Windows APIs, process behavior, network indicators, and why isolation matters. But I am still early in this area.

For this project, I used Codex with GPT-5.5 as an analysis partner. It helped me reason through the static evidence, understand suspicious Windows APIs, map findings to likely capabilities, and organize everything into a cleaner report.

That does not mean I just pasted in a file and accepted whatever AI said. I still had to provide the evidence, ask the right questions, compare outputs, check the results, and decide what the evidence actually showed. AI was useful here, but it was not a replacement for being careful.

## Safety setup

Because the artifacts showed behavior that looked potentially backdoor-capable, I did not want to casually run the program on my own machine.

The review was done in a fresh virtual machine with no outside network connection. I avoided live command-and-control interaction and did not allow outbound communication. I wanted to inspect the program safely without giving it access to my main system or the internet.

That matters because malware analysis can get messy quickly if you start executing unknown software without containment. Even if something turns out to be less severe than expected, it is not worth risking your main system just to find out.

## What was being reviewed

The artifacts included the main application and an installed service payload named `DeviceDiagnosticsHost`.

The reviewed build installed a Windows service:

`PSDeviceDiagnosticsHost`

Displayed as:

`Microsoft PowerShell Diagnostics Device Host`

Installed under:

`C:\Program Files\WindowsPowerShell\Modules\Microsoft.PowerShell.Diagnostics.Device\DeviceDiagnosticsHost.exe`

Configured as:

`Auto` start, running as `LocalSystem`

That alone is already suspicious given the surrounding context. A paid game utility using a Microsoft PowerShell diagnostics-style name is not a great look. Anti-cracking or safety concerns might explain part of the design, but that naming and placement choice makes the software harder for a normal user to understand or notice.

## What the static analysis showed

The main concern was not Discord account linking or HWID checks. Those can be normal for paid software, especially software trying to prevent account sharing.

The concern was the service capability profile.

Static analysis showed code associated with command execution, including APIs and logic related to process creation, output capture, exit code handling, and process termination.

It also showed logic associated with launching processes in the active user session. That included Windows APIs related to identifying the active console session, querying a user token, duplicating tokens, and creating a user environment.

There were also file operation capabilities, including directory enumeration, file reading, file writing, file deletion, directory deletion, and chunk-style transfer fields.

The service also contained screenshot-related capability, including display enumeration and screen capture logic.

On top of that, there were signs of window and process telemetry, including active window detection, window title collection, process enumeration, and related model fields.

System fingerprinting was also supported, with fields and logic for CPU, GPU, RAM, motherboard, OS, computer name, and username.

Discord identity fields were present as well, including fields for Discord ID, name, and email. Again, I would not call that malicious by itself because the app’s business model appears to involve Discord-linked subscriptions. But combined with everything else, it becomes part of a larger identity and system profile.

Finally, static analysis showed network communication capability through HTTP/TCP components, network streams, line-based readers/writers, and JSON serialization/parsing.

I did not confirm live command-and-control traffic, an active remote operator session, or actual data exfiltration. The VM was kept offline. What I did find was remote command-execution capability, host telemetry, file access, screenshot capture, and separate network-communication capability. Finding those capabilities does not prove they were actively used against someone.

That is already enough to treat it as high risk.

## Why anti-cracking does not explain everything

One possible explanation for some of this behavior is licensing enforcement or protection against cracking.

I understand why paid software developers want anti-cracking controls. Developers of paid game utilities may be especially concerned about leaks, resale, reverse engineering, and account sharing. That market is already adversarial.

But there is a line between licensing enforcement and installing a hidden-looking LocalSystem service with broad host control capabilities.

A licensing system can check a subscription. It can validate an HWID. It can verify a Discord account. It can refuse to launch if the user is not authorized.

It does not need to install itself as a PowerShell diagnostics-themed Windows service running as `LocalSystem`.

It does not need screenshot capture.

It does not need broad file read/write/delete capability.

It does not need command execution and output capture.

It does not need process/window telemetry unless there is a very clear and disclosed reason, and even then, that should be documented in a way users can understand.

Could some of those things be explained as anti-tamper or anti-debugging functionality? Maybe partially. But the overall design goes well beyond what I would personally be comfortable running on my system.

## What AI helped with

Codex with GPT-5.5 was useful for making the analysis more structured.

The biggest help was translating scattered static findings into a capability map. Instead of just seeing a list of APIs and fields, I could work through what they usually do, what the static evidence showed, and what would still require dynamic testing to confirm.

It also helped with cautious wording. That part is underrated. In security writing, it is easy to accidentally overstate things. Finding file read and transfer code does not prove that files were stolen. Finding backdoor-like capabilities does not prove that someone actively used them.

That difference matters.

I wanted the final report to separate confirmed findings from supported capabilities and limitations. For example, service persistence was confirmed. Running as `LocalSystem` was confirmed. The presence of command execution-related code was confirmed statically. But live C2 traffic was not confirmed, because the system stayed offline.

That kind of distinction makes the report more credible.

## Limitations

There are a few important limitations.

First, this review covered one supplied build. The findings should not automatically be applied to every version of the software.

Second, no live outbound network traffic was confirmed. The VM was intentionally kept offline for containment.

Third, no active remote operator session was observed.

Fourth, no clear plaintext command-and-control URL was recovered during the static review.

Those limitations do not make the service safe. They just define what was and was not proven.

## My takeaway

This was a useful learning project because it forced me to look past whether something simply seemed suspicious and focus on what the evidence actually showed.

The Discord and HWID pieces were not the main issue. Given the context of a paid game utility, those parts were expected.

The issue was the installed service behavior. It included persistence, LocalSystem execution, command execution capability, file operations, screenshot capture, process and window telemetry, system fingerprinting, and network communication capability.

That combination is far beyond what I would personally accept from a licensing or anti-cracking system, especially when it is installed under a PowerShell diagnostics-themed path.

I still have a lot to learn in malware analysis, but this was a good practical exercise in safe handling, static evidence review, capability mapping, and cautious reporting. It also reinforced why trust matters so much with software that asks for deep access to a system.

Even if the stated goal is anti-cracking or subscription enforcement, users should not have to accept a high-risk service with backdoor-capable functionality just to run an application.
