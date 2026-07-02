# Investigation Notes

## Executive Summary

A Microsoft Defender Antivirus folder exclusion was intentionally created and monitored to understand how Defender records configuration changes. The investigation validated that Event ID 5007 is generated whenever exclusions are added or removed.

This activity demonstrates how defenders can detect unauthorized security configuration modifications that may indicate defense evasion.

---

# Investigation Timeline

| Time | Activity |
|------|----------|
| Folder Created | Created `C:\SOC-Exclusion-Test` |
| Exclusion Added | Added folder as Defender exclusion |
| Validation | Verified exclusion using PowerShell |
| Event Generated | Windows Defender Event ID 5007 |
| Exclusion Removed | Deleted exclusion |
| Validation | Confirmed exclusion removal |

---

# Evidence Collected

## Windows Defender Event Log

Log:

```
Microsoft-Windows-Windows Defender/Operational
```

Event ID:

```
5007
```

Description:

```
Microsoft Defender Antivirus Configuration has changed.
```

Registry Path:

```
HKLM\SOFTWARE\Microsoft\Windows Defender\Exclusions\Paths
```

Excluded Folder:

```
C:\SOC-Exclusion-Test
```

---

## PowerShell Validation

Command:

```powershell
Get-MpPreference | Select ExclusionPath
```

Result:

```
C:\SOC-Exclusion-Test
```

---

## Investigation Findings

The investigation confirmed:

- Defender exclusions are immediately applied.
- Windows Defender logs every configuration change.
- Event ID 5007 records the modified registry path.
- PowerShell accurately reports configured exclusions.
- Removing the exclusion generates another Defender configuration change.

---

# Mini Investigation Scenario

## Scenario

During a routine endpoint review, the SOC team discovered that the following exclusion had been added to Microsoft Defender Antivirus:

```
C:\Users\Public\Downloads
```

No approved change request existed for this modification.

---

## Why This Is Suspicious

Attackers frequently add exclusions before dropping malware or ransomware.

By excluding directories, Microsoft Defender no longer scans files located within those folders.

This allows malicious payloads to remain undetected.

---

## Potential Risks

- Malware execution
- Ransomware staging
- Persistence
- Defense evasion
- Reduced endpoint visibility

---

## SOC Investigation Steps

1. Verify the exclusion using PowerShell.

```powershell
Get-MpPreference | Select ExclusionPath
```

2. Review Windows Defender Operational logs.

3. Investigate Event ID 5007.

4. Determine which account modified Defender settings.

5. Remove unauthorized exclusions.

6. Perform a full antivirus scan.

7. Review PowerShell logs and recently executed processes.

---

## MITRE ATT&CK

Technique:

```
T1562.001
Impair Defenses
```

---

## Analyst Conclusion

Microsoft Defender exclusions should be tightly controlled and regularly audited.

Unexpected exclusions should be treated as potential defense evasion attempts until validated by administrators.

Monitoring Event ID 5007 provides valuable visibility into endpoint security configuration changes.
