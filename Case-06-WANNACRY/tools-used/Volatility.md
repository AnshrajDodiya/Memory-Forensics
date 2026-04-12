
Volatility was used as the primary memory forensics framework for this case study.

It was used to identify the ransomware execution chain, analyze network communication, recover Tor artifacts, detect persistence mechanisms, extract mutexes and loaded modules, dump malicious processes, and recover ransomware IOCs from memory.

---

## Commands Used

```bash
python2 vol.py -f wanncry.vmem imageinfo
python2 vol.py -f wanncry.vmem --profile Win7SP1x64 pstree
python2 vol.py -f wanncry.vmem --profile Win7SP1x64 cmdline -p 2464,2340,2752,2092,2664
python2 vol.py -f wanncry.vmem --profile Win7SP1x64 netscan
python2 vol.py -f wanncry.vmem --profile Win7SP1x64 handles -t FILE -p 2092
python2 vol.py -f wanncry.vmem --profile Win7SP1x64 handles -t FILE -p 2464
python2 vol.py -f wanncry.vmem --profile Win7SP1x64 handles -t FILE -p 2752
python2 vol.py -f wanncry.vmem --profile Win7SP1x64 dlllist -p 2092
python2 vol.py -f wanncry.vmem --profile Win7SP1x64 dlllist -p 2464
python2 vol.py -f wanncry.vmem --profile Win7SP1x64 dlllist -p 2340
python2 vol.py -f wanncry.vmem --profile Win7SP1x64 handles -t MUTANT -p 2464
python2 vol.py -f wanncry.vmem --profile Win7SP1x64 ldrmodules -p 2752
python2 vol.py -f wanncry.vmem --profile Win7SP1x64 ldrmodules -p 2092
python2 vol.py -f wanncry.vmem --profile Win7SP1x64 ldrmodules -p 2340
python2 vol.py -f wanncry.vmem --profile Win7SP1x64 printkey -K "software\microsoft\windows\currentversion\run"
python2 vol.py -f wanncry.vmem --profile Win7SP1x64 procdump -p 2340,2092,2464,2752 -D Malicious-Objects/
```

---

## Key Artifacts Recovered

- Suggested profile: `Win7SP1x64`
- Ransomware process chain:
  - `WannaCry.EXE`
  - `@WanaDecryptor`
  - `taskhsvc.exe`
- Tor service artifacts
- onion domain IOCs
- bitcoin ransom note strings
- persistence Run key
- dumped ransomware binaries
- hidden module anomalies
- mutex artifacts
- encryption indicators (`.eky`, `.WNCRYT`)

---

## Major Forensic Evidence

### Process Chain

```text
explorer.exe
 ├── WannaCry.EXE
 ├── @WanaDecryptor
 └── taskhsvc.exe
```

---

### Persistence

```text
C:\Users\labib\Desktop\tasksche.exe
```

---

### IOC Evidence

```text
57g7spgrzlojinas.onion
gx7ekbenv2riucmf.onion
Send $300 worth of bitcoin
```