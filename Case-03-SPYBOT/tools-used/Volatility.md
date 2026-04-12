
Volatility was used as the primary memory forensics framework for this case study.

It helped identify suspicious processes, recover command-line artifacts, inspect network communication, analyze mutex handles, and extract the malicious executable from memory.

---

## Commands Used

```bash
python2 vol.py -f spybot.vmem imageinfo
python2 vol.py -f spybot.vmem pstree
python2 vol.py -f spybot.vmem cmdline -p 1688,1676,1700
python2 vol.py -f spybot.vmem connscan
python2 vol.py -f spybot.vmem handles -t MUTANT -p 1676,1700,1688
python2 vol.py -f spybot.vmem procdump -p 1700 -D Malicious-Objects
sha256sum executable.1700.exe
```

---

## Key Artifacts Recovered

- Suggested profile: `WinXPSP3x86`
- Suspicious process chain
- Command-line execution path
- External network connection
- Mutex artifact: `krnel`
- Malicious PE dump