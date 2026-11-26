# 📡 Nmap & Varreduras de Rede

---

## 🔄 Fluxograma de Enumeração

```
PORTAS → SERVIÇOS → VERSÕES → DIRETÓRIOS → SUBDOMÍNIOS → VULNERABILIDADES
```

---

## 1. Escaneamento em Duas Fases (Recomendado no Exame)

```bash
# FASE 1: Descobrir rapidamente TODAS as portas abertas (0 a 65535)
sudo nmap -p- -Pn -vv --min-rate=1000 -oA nmap-portscan IP_ALVO

# FASE 2: Escaneamento detalhado somente nas portas abertas identificadas
nmap -p $(cat nmap-portscan.nmap | grep open | cut -d '/' -f1 | tr '\n' ',' | sed 's/,$//') -sV -sC -O --script=vuln -oA nmap-detalhado IP_ALVO
```

---

## 2. Varreduras em Blocos de Rede (Subnet Scanning)

```bash
# Varredura rápida para descobrir quais hosts estão ativos na sub-rede
nmap -sn 192.168.1.0/24 -oG hosts.txt
grep "Up" hosts.txt | cut -d " " -f2 > hosts_ativos.txt

# Varredura direcionada em porta específica nos hosts vivos
nmap -sS -p 445 --open -Pn -iL hosts_ativos.txt -oG smb.txt
```

---

## 3. Comandos e Flags Essenciais do Nmap

```bash
nmap -sT -p 80 IP_ALVO              # TCP Connect Scan (completa handshake 3-way)
nmap -sS -p 80 IP_ALVO              # SYN Scan (Half-Open) - Rápido e furtivo
nmap -sU -p 69 IP_ALVO              # UDP Scan
nmap -O IP_ALVO                     # Deteção de Sistema Operacional (OS Fingerprinting)

# Scripts NSE direcionados
nmap -p21 --script ftp-vsftpd-backdoor.nse -Pn IP_ALVO
nmap -p80 --script http-shellshock --script-args uri=/cgi-bin/test.cgi,cmd=ls IP_ALVO

# Salvar simultaneamente em formato Normal, XML e Grepable (-oA)
nmap -oN saida.txt -oX saida.xml -oG saida.gnmap IP_ALVO
```

---

> [!tip] Navegação
> - Voltar para: [[DCPT|Master MOC DCPT]]
> - Próximo: [[02 - Gobuster & Enumeração Web]]
