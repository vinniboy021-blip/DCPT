# 🌐 Gobuster & Enumeração Web

---

## 1. Modo Diretório (`gobuster dir`)

Realizar brute force de diretórios e arquivos em serviços Web com extensão especificada:

```bash
gobuster dir -u http://IP_ALVO/ \
  -w /usr/share/wordlists/dirb/big.txt \
  -r -k -t 100 -e --no-error \
  -o gobuster \
  -a "Mozilla/5.0" \
  -x php,bkp,old,txt,xml,cgi,pdf,html,htm,asp,aspx,pl,sql,js
```

### Explicação das Flags
- `-u`: URL do alvo
- `-w`: Caminho da wordlist
- `-r`: Seguir redirecionamentos HTTP
- `-k`: Ignorar erros de certificado SSL/TLS
- `-t 100`: 100 threads simultâneas
- `-x`: Extensões de arquivos para testar em paralelo
- `-a`: User-Agent customizado

---

## 2. Modo DNS / Subdomínios (`gobuster dns`)

Descobrir subdomínios via resolução DNS:

```bash
gobuster dns -d dominio.com \
  -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt \
  -t 30
```

---

> [!tip] Navegação
> - Voltar para: [[DCPT|Master MOC DCPT]]
> - Anterior: [[01 - Nmap & Varreduras de Rede]] | Próximo: [[03 - Enumeração de Serviços (SMB, SMTP, SNMP, NFS, SSH, MySQL)]]
