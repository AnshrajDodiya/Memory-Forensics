
VirusTotal was used to validate the dumped WannaCry ransomware executable using its SHA256 hash.

This helped confirm the malware family and strengthen the final forensic conclusion.

---

## Hash Submitted

```text
e1e45be4e808bc12d5c3cbd8761e44cb333d4b027e720f59475f0cb144faa8d8
235778b9b1d3b60276e17646114ace4d045d4e0d4f9bf2fd30581af79943b9b8
8e21f985762d0d6a762a6396daf178f3d94eabdcb7e7bb08de09eee78731850f
41708218c8b993aed497fd56b335ecc83d3e8af9455b61636ca7d43d78dc3dec
```

---

## Detection Result

- Detection ratio: **67/71**
- Malware classification: **WannaCry / WannaCryptor**
- Threat category: **Ransomware**

---

## Threat Intelligence Validation

Popular labels observed:

- `wannacry`
- `wannacryptor`
- `ransomware`

This strongly validates the memory forensic findings.

---

## Supporting Evidence

The VirusTotal result aligns with:

- Tor onion IOC recovery
- bitcoin ransom strings
- persistence artifacts
- encryption evidence
- ransomware execution chain