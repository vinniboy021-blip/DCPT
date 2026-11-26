# 🛠️ Enumeração de Serviços Específicos

---

## 1. SMTP (Portas 25 / 465 / 587)

Verificar se comandos de enumeração de usuário (`VRFY`, `EXPN`) estão habilitados no servidor de e-mail.

```bash
# Conexão manual via Netcat
nc -nv IP_ALVO 25
HELO test
VRFY root
VRFY admin
VRFY www-data
```

### Script Python para Automação SMTP (VRFY):

```python
import socket, sys

if len(sys.argv) != 3:
    print("Modo de uso: python script.py IP USUARIO")
    sys.exit(0)

tcp = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
tcp.connect((sys.argv[1], 25))
banner = tcp.recv(1024)
print(banner)
tcp.send("VRFY " + sys.argv[2] + "\r\n")
user = tcp.recv(1024)
print(user)
tcp.close()
```

---

## 2. SMB / NetBIOS (Portas 139 / 445)

```bash
# Listar compartilhamentos sem senha (Sessão Nula / Anônima)
smbclient -L \\\\IP_ALVO -N

# Conectar em um compartilhamento específico
smbclient //IP_ALVO/COMPARTILHAMENTO -N

# Enumeração completa automatizada
enum4linux -a IP_ALVO
enum4linux -U IP_ALVO     # Enumeração de usuários
enum4linux -S IP_ALVO     # Enumeração de compartilhamentos
```

---

## 3. SNMP (Porta UDP 161)

```bash
# Descobrir community strings conhecidas
onesixtyone -c /usr/share/wordlists/seclists/Discovery/SNMP/common-snmp-community-strings.txt IP_ALVO

# Consultar MIBs SNMP
snmpwalk -c public -v1 IP_ALVO 1.3.6.1.2.1.1                 # Walk na árvore de sistema
snmpwalk -c public -v1 IP_ALVO 1.3.6.1.4.1.77.1.2.25        # Enumerar contas de usuários
snmp-check IP_ALVO -c public                                 # Relatório completo formatado
```

---

## 4. NFS (Porta 2049)

```bash
# Listar diretórios exportados
showmount -e IP_ALVO

# Montar compartilhamento remoto no diretório local
mkdir /mnt/nfs
mount -t nfs -o vers=3,proto=tcp,nolock IP_ALVO:/pasta /mnt/nfs
```

---

## 5. MySQL (Porta 3306)

```bash
mysql -h IP_ALVO -u root -p
# Comandos SQL úteis:
# SHOW DATABASES; USE nome_db; SHOW TABLES; SELECT * FROM usuarios;
```

---

## 6. SSH (Porta 22)

```bash
nc -nv IP_ALVO 22       # Banner grabbing
ssh -v IP_ALVO          # Executar com verbose para inspecionar algoritmos suportados
```

---

> [!tip] Navegação
> - Voltar para: [[DCPT|Master MOC DCPT]]
> - Anterior: [[02 - Gobuster & Enumeração Web]] | Próximo: [[04 - DNS, Subdomínios & WAF]]
