# Troubleshooting Notes

## Issue 1

### Problem

Folder exclusion did not immediately appear in PowerShell.

### Cause

Microsoft Defender settings had not refreshed.

### Resolution

Run:

```powershell
Get-MpPreference | Select ExclusionPath
```

or reopen Windows Security.

---

## Issue 2

### Problem

Event ID 5007 was not immediately visible.

### Cause

Windows Defender Operational log refresh delay.

### Resolution

Refresh Event Viewer or reopen:

```
Applications and Services Logs
    Microsoft
        Windows
            Windows Defender
                Operational
```

---

## Issue 3

### Problem

Unable to find the registry location.

### Cause

Incorrect registry path.

### Correct Location

```
HKLM\SOFTWARE\Microsoft\Windows Defender\Exclusions\Paths
```

---

## Issue 4

### Problem

PowerShell returned an empty exclusion list.

### Cause

The exclusion had already been removed.

### Resolution

Create a new exclusion and rerun:

```powershell
Get-MpPreference | Select ExclusionPath
```

---

## Issue 5

### Problem

Folder exclusion remained after investigation.

### Cause

The exclusion was not manually removed.

### Resolution

Navigate to:

```
Windows Security

→ Virus & threat protection

→ Manage Settings

→ Exclusions

→ Remove
```

or execute:

```powershell
Remove-MpPreference -ExclusionPath "C:\SOC-Exclusion-Test"
```

---

# Lessons Learned

- Defender exclusions generate Event ID 5007.
- PowerShell provides quick validation of Defender settings.
- Registry changes correspond directly to Defender exclusions.
- Unauthorized exclusions represent a common defense evasion technique.
- Regular auditing of Defender configuration is an important SOC monitoring activity.
