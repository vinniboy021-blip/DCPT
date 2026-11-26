# 🔍 DNS, Subdomínios & WAF

---

## 1. Transferência de Zona DNS (AXFR)

Testar se os DNS Servers autoritativos permitem transferência de zona sem autenticação:

```bash
for server in $(host -t ns dominio.com | cut -d " " -f7); do
    host -l -a dominio.com $server
done
```

---

## 2. Bruteforce de Subdomínios via Terminal

```bash
for domain in $(cat /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt); do
    host -t a $domain.dominio.com | grep -v "NXDOMAIN"
done
```

---

## 3. Identificação de WAF (Web Application Firewall)

Identificar se o alvo está atrás de um WAF (Cloudflare, ModSecurity, AWS WAF, etc.):

```bash
wafw00f IP_ALVO
```

---

> [!tip] Navegação
> - Voltar para: [[DCPT|Master MOC DCPT]]
> - Anterior: [[03 - Enumeração de Serviços (SMB, SMTP, SNMP, NFS, SSH, MySQL)]]
