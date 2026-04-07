# Volatility

## Purpose

Volatility was used as the primary tool for analyzing the CRIDEX memory image.

It was used to identify suspicious processes, extract malware artifacts, inspect registry hives, and analyze network connections.

---

## Key Commands Used

```bash
python2 vol.py -f cridex.vmem imageinfo
python2 vol.py -f cridex.vmem --profile=WinXPSP2x86 pstree
python2 vol.py -f cridex.vmem --profile=WinXPSP2x86 cmdline
python2 vol.py -f cridex.vmem --profile=WinXPSP2x86 dlllist -p 1640
python2 vol.py -f cridex.vmem --profile=WinXPSP2x86 procdump -p 1640 -D Malicious-Objects/
python2 vol.py -f cridex.vmem --profile=WinXPSP2x86 dumpregistry -o 0xe1a19b60 -D Malicious-Objects/
python2 vol.py -f cridex.vmem --profile=WinXPSP2x86 hivelist
python2 vol.py -f cridex.vmem --profile=WinXPSP2x86 printkey -K "software\microsoft\windows\currentversion\run"
python2 vol.py -f cridex.vmem --profile=WinXPSP2x86 connscan
python2 vol.py -f cridex.vmem --profile=WinXPSP2x86 sockets
sha256sum Malicious-Objects/executable.1640.exe
strings Malicious-Objects/executable.1640.exe
```

---

## Why These Plugins

- ## Why These Commands

- `imageinfo` → Used to identify the correct operating system profile, kernel type, and memory image metadata before beginning analysis.
    
- `pstree` → Used to visualize the parent-child process hierarchy and identify suspicious process relationships, which helped isolate `reader_sl.exe` as a malicious process.
    
- `cmdline` → Used to inspect the command-line arguments and executable paths of active processes to validate the location and legitimacy of the suspicious executable.
    
- `dlllist -p 1640` → Used to enumerate all DLLs and loaded modules associated with the suspicious process (PID 1640) to identify abnormal libraries or injected components.
    
- `procdump -p 1640 -D Malicious-Objects/` → Used to extract the malicious executable directly from memory for further static analysis, hashing, and reputation validation.
    
- `dumpregistry -o 0xe1a19b60 -D Malicious-Objects/` → Used to extract the specific registry hive from memory using its virtual offset for offline persistence analysis.
    
- `hivelist` → Used to enumerate all registry hives loaded in memory and identify the correct hive offsets before dumping and analyzing them.
    
- `printkey -K "software\microsoft\windows\currentversion\run"` → Used to inspect the Run key for autorun entries and validate malware persistence mechanisms.
    
- `connscan` → Used to scan memory for historical and active TCP connection objects, helping identify suspicious external communication and possible C2 infrastructure.
    
- `sockets` → Used to enumerate open sockets and confirm active network communication from the infected host.
    
- `sha256sum Malicious-Objects/executable.1640.exe` → Used to generate the SHA256 hash of the dumped executable for integrity validation and threat intelligence correlation.
    
- `strings Malicious-Objects/executable.1640.exe` → Used to extract human-readable strings from the dumped PE file to identify suspicious filenames, IP addresses, registry APIs, and banking-related artifacts.
