Volatility was used as the primary memory forensics framework for this case study.

It was used to identify suspicious processes, inspect network artifacts, validate service execution, detect injected DLLs, identify hidden modules, and extract the malicious DLL from memory.

---

## Commands Used

```bash
python2 vol.py -f zegost.vmem imageinfo
python2 vol.py -f zegost.vmem --profile Win7SP1x86 pstree
python2 vol.py -f zegost.vmem --profile Win7SP1x86 netscan
python2 vol.py -f zegost.vmem --profile Win7SP1x86 cmdline -p 880
python2 vol.py -f zegost.vmem --profile Win7SP1x86 dlllist -p 880 | grep -iF ".ddf" --color
python2 vol.py -f zegost.vmem --profile Win7SP1x86 ldrmodules -p 880 | grep -i "False"
python2 vol.py -f zegost.vmem --profile Win7SP1x86 dlldump -p 880 -b 0x10000000 -D Malicious-Objects/
```

---

## Key Artifacts Recovered

- Suggested profile: `Win7SP1x86`
- Suspicious process: `svchost.exe`
- Network connection: `192.168.1.22:8000`
- Injected DLL: `imageik.ddf`
- Hidden / unlinked module
- Extracted malicious DLL