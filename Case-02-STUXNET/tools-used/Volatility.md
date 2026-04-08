
## Overview
  
**Volatility Framework** is an advanced open-source memory forensics tool used to analyze RAM dumps and extract forensic artifacts from volatile memory.

In this project, **Volatility 2.6.1** was used to investigate the `stuxnet.vmem` memory image.

---
## Purpose in This Investigation

Volatility was used to:

- identify the correct memory profile

- enumerate active processes

- inspect command-line arguments

- analyze active sockets and connections

- detect injected memory regions

- dump suspicious processes

---
## Commands Used

### Image Profile Identification

**python2 vol.py -f stuxnet.vmem imageinfo**

### Process Tree Analysis

**python2 vol.py -f stuxnet.vmem --profile WinXPSP2x86 pstree**

### Command Line Inspection

**python2 vol.py -f stuxnet.vmem --profile WinXPSP2x86 cmdline -p 680,868,1928**

### Socket Analysis

**python2 vol.py -f stuxnet.vmem --profile WinXPSP2x86 sockets**

### DLL Count

**python2 vol.py -f stuxnet.vmem --profile WinXPSP2x86 dlllist -p 680 | wc -l**

**python2 vol.py -f stuxnet.vmem --profile WinXPSP2x86 dlllist -p 868 | wc -l**

**python2 vol.py -f stuxnet.vmem --profile WinXPSP2x86 dlllist -p 1928 | wc -l**

### DLL Validation

**python2 vol.py -f stuxnet.vmem --profile WinXPSP2x86 dlllist -p 680 | grep -iF "netlogon"

**python2 vol.py -f stuxnet.vmem --profile WinXPSP2x86 dlllist -p 868 | grep -iF "netlogon"**

**python2 vol.py -f stuxnet.vmem --profile WinXPSP2x86 dlllist -p 1928 | grep -iF "netlogon"**

(**Did Same for the Kerberos dll**)

### Injection Detection

**python2 vol.py -f stuxnet.vmem --profile WinXPSP2x86 malfind -p 868,1928**

### Process Dumping

**python2 vol.py -f stuxnet.vmem --profile WinXPSP2x86 procdump -p 1928,868,940,668,600,1196** **-D Malicious-Objects/** 

### Hash Generation

**(md5sum * )** // To Generate Hash of all Dumped Processes







