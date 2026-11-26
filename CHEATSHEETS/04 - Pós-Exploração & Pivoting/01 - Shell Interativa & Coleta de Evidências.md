# 🐚 Shell Interativa & Coleta de Evidências

---

## 1. Estabilização de Shell (PTY Upgrade)

> [!important] Shells cegas/simplificadas podem fechar em comandos interativos (ex: `su`, `sudo`, `vim`). Sempre estabilize a shell logo após a invasão.

### Linux
```bash
# Método 1: Python PTY Spawn
python3 -c 'import pty;pty.spawn("/bin/bash")'

# Método 2: Bash Interativo
/bin/bash -i

# Método 3: Script Command
/usr/usr/bin/script -qc /bin/bash /dev/null

# Passo Final (Ajuste de Terminal stty):
# 1. Pressione Ctrl+Z para suspender a shell
# 2. No seu terminal local: stty raw -echo; fg
# 3. Digite: reset; export TERM=xterm-256color
```

### Windows
```cmd
powershell -c Start-Process cmd -Verb RunAs
```

---

## 2. Coleta de Evidências para Relatório

Execute e tire screenshot dos seguintes comandos para validação das flags:

### Evidências em Alvos Linux
```bash
id && hostname && uname -a && cat /etc/os-release
ifconfig; netstat -anpt; sudo -l
cat /root/proof.txt 2>/dev/null || cat /root/root.txt
```

### Evidências em Alvos Windows
```cmd
whoami && hostname && systeminfo
ipconfig /all; netstat -ano; net user
type C:\Users\Administrator\Desktop\proof.txt
```