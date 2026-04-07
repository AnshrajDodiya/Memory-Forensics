# Technical Findings — Case 01 CRIDEX

## Case Summary

A memory forensic investigation was performed on the CRIDEX memory image using Volatility.

The analysis confirmed the presence of **banking malware with persistence and active external communication**.

---

## Key Findings

### 1. Suspicious Process

A suspicious process was identified:

```text
reader_sl.exe
PID: 1640
Parent: explorer.exe
PPID: 1484
```

The process masquerades as a legitimate Adobe Reader component.

---

### 2. Malware Extraction

The malicious process was successfully dumped from memory using Volatility’s `procdump` plugin.

The extracted PE was hash-validated and correlated with known malicious signatures.

---

### 3. Persistence

Persistence was confirmed through the following registry Run key:

```text
Software\Microsoft\Windows\CurrentVersion\Run
```

Malicious value:

```text
KB00207877.exe
```

Full path observed:

```text
C:\Documents and Settings\Robert\Application Data\KB00207877.exe
```

This ensures malware execution at user logon.

---

### 4. Network Indicators

Suspicious outbound connections were identified:

```text
41.168.5.140:8080
125.19.103.198:8080
```

These IPs strongly indicate possible C2 communication.

---

### 5. Behavioral Indicators

String analysis revealed:

- registry API calls
    
- suspicious executable filename
    
- C2 IP artifacts
    
- banking institution references
    

These artifacts strongly support the classification as a **banking trojan**.

---

## Final Assessment

The sample is classified as **CRIDEX banking malware** with:

- malicious process execution
    
- persistence via Run key
    
- external C2 communication
    
- banking credential theft behavior