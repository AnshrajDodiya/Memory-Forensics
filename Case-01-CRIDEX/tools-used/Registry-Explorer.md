# Registry Explorer

## Purpose

Registry Explorer was used to analyze the extracted `NTUSER.DAT` hive offline.

This helped validate registry persistence mechanisms identified in memory.

---

## Key Finding

The following Run key was identified:

```text
Software\Microsoft\Windows\CurrentVersion\Run
```

Suspicious autorun value:

```text
KB00207877.exe
```

Full path:

```text
C:\Documents and Settings\Robert\Application Data\KB00207877.exe
```

This confirms user logon persistence.