# microsoft-defender-lab07-defender-exclusions-investigation
## Overview

Microsoft Defender Antivirus allows administrators to configure exclusions for files, folders, processes, and file extensions. While exclusions are useful for preventing false positives, unauthorized exclusions are commonly abused by attackers to evade antivirus detection.

This lab demonstrates how to create, verify, monitor, and remove Defender exclusions while investigating the corresponding Windows Defender Operational logs.

---

## Objectives

- Create a Microsoft Defender folder exclusion
- Verify exclusions using PowerShell
- Monitor Defender configuration changes
- Investigate Event ID 5007
- Remove exclusions
- Understand how exclusions can be abused by attackers

---

## Lab Environment

- Windows 10 Virtual Machine
- Microsoft Defender Antivirus
- Windows Event Viewer
- PowerShell

---

## Steps Performed

1. Created a test folder (`C:\SOC-Exclusion-Test`)
2. Added the folder as a Defender exclusion
3. Verified the exclusion using:

```powershell
Get-MpPreference | Select ExclusionPath
```

4. Reviewed Windows Defender Operational logs
5. Investigated Event ID 5007
6. Removed the exclusion
7. Verified successful removal

---

## Key Findings

- Defender exclusions immediately generate configuration change events.
- Event ID 5007 records Defender configuration modifications.
- PowerShell can be used to validate current exclusions.
- Unauthorized exclusions may indicate attacker defense evasion.

---

## MITRE ATT&CK Mapping

| Technique | ID |
|----------|------|
| Impair Defenses | T1562.001 |

---

## Skills Practiced

- Microsoft Defender Administration
- Windows Event Viewer
- PowerShell
- Security Monitoring
- Endpoint Investigation
- SOC Documentation
- MITRE ATT&CK Mapping

---

## Learning Outcomes

- Understand Defender exclusion behavior
- Investigate configuration change events
- Validate Defender settings using PowerShell
- Recognize potential defense evasion techniques
- Document endpoint security investigations
