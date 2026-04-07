# VirusTotal

## Purpose

VirusTotal was used to validate the SHA256 hash of the dumped malicious PE.

This step was performed after extracting the executable from memory.

---

## Detection Result

The submitted hash was flagged by:

```text
28 / 71 vendors
```

This confirms the file is malicious.

---

## Threat Classification

The sample was identified as:

- trojan
    
- banking malware
    
- credential stealing malware
    

This aligns with the CRIDEX banking trojan behavior observed during analysis.