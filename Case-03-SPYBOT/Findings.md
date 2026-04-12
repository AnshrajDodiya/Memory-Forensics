# Technical Findings — Case 03 SPYBOT

## Case Summary

A memory forensic investigation was performed on the Spybot memory image using Volatility.

The analysis confirmed the presence of **IRC bot malware with process masquerading, active external communication, and a malicious in-memory payload**.

---

## Key Findings

### 1. Suspicious Process Chain

A suspicious process chain was identified during process tree analysis:

```text
VMwareUser.exe
   └── scvhost.exe   (Exited)
          └── wuaumqr.exe 
```
---
### 2. Command Line Evidence

Command-line analysis confirmed the execution path of the malicious payload.

**C:\WINDOWS\system32\wuaumqr.exe**

This confirms successful execution of the malware from the `system32` directory.

---

### 3. Network Indicators

Suspicious outbound communication was identified.

Local: 192.168.1.100:1033  
Remote: 209.126.201.22:6667

Key observations:

- external communication established successfully
- port `6667` strongly suggests **IRC-based C2 communication**
- connection associated with `wuaumqr.exe`

---

### 4. Mutex Artifact

A suspicious mutex handle was identified:

**`krnel`**

This mutex is associated with the malicious process and likely ensures single-instance execution.

---

### 5. Malware Extraction

The malicious process was successfully dumped from memory using Volatility’s **`procdump`** plugin.

The dumped PE was hash-validated successfully.

---

### 6. Hash Validation

SHA256:

**`f6faaeebab3c4aace13efde94a5eb7e5aaeef2c108e90d183cc246d0f7e77a1`**

VirusTotal confirmed the sample as **Spybot malware / IRC bot**.

