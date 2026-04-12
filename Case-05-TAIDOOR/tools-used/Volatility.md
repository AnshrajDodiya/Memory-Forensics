
Volatility was used as the primary memory forensics framework for this case study.

It was used to identify suspicious processes, analyze network communication, detect injected memory regions, validate process hollowing, inspect mutex artifacts, and extract the malicious payload from memory.

---

## Commands Used

```bash
python2 vol.py -f taidoor.vmem imageinfo
python2 vol.py -f taidoor.vmem --profile Win7SP1x86 pstree
python2 vol.py -f taidoor.vmem --profile Win7SP1x86 netscan
python2 vol.py -f taidoor.vmem --profile Win7SP1x86 cmdline -p 1412
python2 vol.py -f taidoor.vmem --profile Win7SP1x86 malfind -p 1412
python2 vol.py -f taidoor.vmem --profile Win7SP1x86 dlllist -p 1412 | grep -i cry
python2 vol.py -f taidoor.vmem --profile Win7SP1x86 handles -t MUTANT -p 1412
python2 vol.py -f taidoor.vmem --profile Win7SP1x86 hollowfind -p 1412
python2 vol.py -f taidoor.vmem --profile Win7SP1x86 procdump -p 1412 -D Malicious-Objects/
```

---

## Key Artifacts Recovered

- Suggested profile: `Win7SP1x86`
- Suspicious process: `svchost.exe`
- Injected PE region at `0x400000`
- Process hollowing evidence
- Multiple mutex artifacts
- Extracted malicious payload