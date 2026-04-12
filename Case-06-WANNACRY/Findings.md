# Technical Findings — Case 06 WANNACRY

## Case Summary

A memory forensic investigation was performed on the WannaCry memory image using Volatility.

The analysis confirmed active **ransomware execution, Tor-based communication, persistence, encryption artifacts, ransom note indicators, and strong IOC evidence**.

---

## Key Findings

### 1. Ransomware Process Chain

Recovered process chain:

```text
explorer.exe
 ├── WannaCry.EXE
 ├── @WanaDecryptor
 ├── @WanaDecryptor
 └── taskhsvc.exe
```

This confirms active ransomware staging and decryption interface.

---

### 2. Network Indicators

Suspicious outbound communication identified:

```text
94.130.200.167:443
51.81.93.162:443
83.212.99.68:443
204.11.50.131:9001
82.149.227.236:9001
131.188.40.189:443
```

These strongly indicate **Tor relay / C2 infrastructure**.

---

### 3. Encryption Indicators

Recovered encrypted artifacts:

```text
00000000.eky
hibsys.WNCRYT
```

This confirms active file encryption.

---

### 4. Persistence

Registry Run key recovered:

```text
C:\Users\labib\Desktop\tasksche.exe
```

This confirms startup persistence.

---

### 5. IOC Evidence

Recovered onion domains:

```text
57g7spgrzlojinas.onion
gx7ekbenv2riucmf.onion
```

Recovered ransom note strings:

```text
Send $300 worth of bitcoin
```

This strongly confirms WannaCry ransom note logic.

---

### 6. Malware Validation

VirusTotal confirmed:

```text
67/71 detections
```

Classification:

- WannaCry
- WannaCryptor
- Ransomware

---

## Final Assessment

The sample is conclusively identified as **WannaCry ransomware** with:

- Tor communication
- ransomware execution chain
- persistence
- ransom note strings
- onion IOC artifacts
- encryption evidence