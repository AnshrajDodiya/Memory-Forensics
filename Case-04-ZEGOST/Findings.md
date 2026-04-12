# Technical Findings — Case 04 ZEGOST

## Case Summary

A memory forensic investigation was performed on the Zegost memory image using Volatility.

The analysis confirmed the presence of **trojan malware utilizing DLL injection, hidden module artifacts, suspicious network activity, and malicious service-based behavior**.

---

## Key Findings

### 1. Suspicious Process

A suspicious process was identified during process tree analysis:

```text
svchost.exe
PID: 880
```

Although `svchost.exe` is a legitimate Windows process, this instance was selected for deeper analysis due to suspicious DLL loading and abnormal network artifacts.

---

### 2. Network Indicators

Suspicious network activity was identified.

```text
Local: 192.168.1.60:49157
Remote: 192.168.1.22:8000
State: CLOSED
```

Key observations:

- communication associated with **`svchost.exe`**
- suspicious outbound connection detected
- possible C2 or lateral communication activity

---

### 3. Command Line Evidence

Command-line validation confirmed the service context.

```text id="g5e4pm"
C:\Windows\system32\svchost.exe -k netsvcs
```

This confirms that the suspicious process was operating under the **`netsvcs`** service group.

---

### 4. Suspicious DLL Injection

DLL analysis revealed a suspicious injected module.

```text id="e7m3ah"
imageik.ddf
```

Loaded from:

```text id="1j5m6c"
C:\Users\test\Application Data\ACD Systems\ACDSee\imageik.ddf
```

This strongly indicates malicious DLL injection into `svchost.exe`.

---

### 5. Hidden / Unlinked Module

Further validation using `ldrmodules` identified an unlinked DLL module.

Multiple flags were marked **False**, strongly indicating:

- hidden module behavior
- manual DLL mapping
- stealth / defense evasion techniques

---

### 6. Malware Extraction

The malicious DLL was successfully extracted from memory using Volatility’s `dlldump` plugin.

Extracted module:

```text id="j76fqd"
module.880.ea13030.10000000.dll
```

PE header validation confirmed a valid executable DLL.

---

### 7. Static DLL Analysis

Post-extraction analysis of the DLL revealed:

- utilization of **`netsvcs`**
- multiple suspicious functions / API references
- embedded malicious domain names
- network-related artifacts

These findings strongly validate the DLL as the malicious payload associated with Zegost.

---

### 8. Hash Validation

SHA256:

```text id="x9c2tr"
c18f5d1249171ff701da3c6b0159b365c11bdc26af506afd422ba0e1f4bd566b
```

VirusTotal confirmed:

```text id="az5g6u"
57/72 detections
```

Malware family:

```text id="gsczzy"
Zegost
```

---

## Final Assessment

The sample is classified as **Zegost Trojan malware** with:

- DLL injection
- hidden module behavior
- suspicious network communication
- service-based persistence
- malicious embedded domains
- confirmed threat intelligence validation