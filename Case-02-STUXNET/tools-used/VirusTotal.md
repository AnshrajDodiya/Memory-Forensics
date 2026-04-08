
## Overview

**VirusTotal** is a malware intelligence and reputation analysis platform used to validate suspicious files through multi-engine antivirus detection.

In this project, dumped process artifacts extracted from memory were uploaded for reputation analysis.

---
## Purpose in This Investigation

VirusTotal was used to:

- validate dumped binaries

- confirm malware family

- compare detection labels

- strengthen forensic confidence

---  
## Files Analyzed

- `executable.868.exe`

- `executable.1196.exe`

- `executable.1928.exe`

- `executable.600.exe`

- `executable.668.exe`

---
## Detection Results

The uploaded samples were flagged by multiple engines.

Common family names observed:

- `Stuxnet`

- `Duqu`

- `Ulise`

This strongly confirmed that the dumped executables were malicious.

---
## Investigation Value

VirusTotal validation helped correlate in-memory artifacts with known malware signatures, confirming the forensic findings from Volatility.

___
