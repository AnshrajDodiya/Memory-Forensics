
# Technical Findings — Case 05 TAIDOOR

## Case Summary

A memory forensic investigation was performed on the Taidoor memory image using Volatility.

The analysis confirmed the presence of **trojan malware utilizing process hollowing, injected executable regions, suspicious network communication, and malicious payload execution**.

---

## Key Findings

### 1. Suspicious Process

A suspicious process was identified:

```text
svchost.exe
PID: 1412
```

Although `svchost.exe` is a legitimate Windows process, this instance showed strong indicators of compromise.

---

### 2. Network Indicators

Suspicious outbound communication was identified.

```text id="m6c4nh"
Local: 192.168.1.60:49161
Remote: 200.2.126.61:443
State: CLOSED
```

This strongly indicates possible **C2 communication**.

---

### 3. Injected Memory Region

Memory analysis using `malfind` revealed:

- executable region at **`0x400000`**
- valid **MZ header**
- injected PE artifact in memory

This strongly supports in-memory code injection.

---

### 4. Process Hollowing

Process hollowing was confirmed using `hollowfind`.

Key observations:

- base address discrepancy
- protection mismatch
- injected executable memory region
- suspicious PE payload replacement

This confirms **process hollowing / defense evasion behavior**.

---

### 5. Mutex Artifacts

Multiple mutex artifacts were recovered.

Examples include:

```text id="2f3t4q"
WininetStartupMutex
WininetConnectionMutex
WininetProxyRegistryMutex
```
These indicate malware runtime control and synchronization.

``` text
RasPbFile
```
This Mutex Also Seems Suspicious.

---

### 6. Malware Extraction

The suspicious process was successfully dumped.

```text id="q1n7ze"
executable.1412.exe
```

---

### 7. Hash Validation

SHA256:

```text id="e0g4vd"
e5d60ec098adb0d867216d80d6cef9d6398d13c162efa9904590ee6215b2e85d
```

VirusTotal confirmed:

```text id="p7h5sj"
57/69 detections
```

Classification:

- Trojan
- Downloader
- Backdoor

---

## Final Assessment

The sample is classified as **Taidoor malware** with:

- process hollowing
- injected PE region
- suspicious C2 communication
- runtime mutex control
- malicious payload validation