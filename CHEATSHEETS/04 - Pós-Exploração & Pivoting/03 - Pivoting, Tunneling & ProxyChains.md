# 🔀 Pivoting, Tunneling & ProxyChains

---

## 1. Autoroute e SOCKS Proxy no Metasploit

Quando você obtém uma sessão em uma máquina dual-homed (com acesso a uma rede interna oculta):

```bash
# Adicionar rota para a sub-rede interna
run autoroute -s 10.10.20.0/24

# Subir servidor de SOCKS Proxy no Metasploit
use auxiliary/server/socks_proxy
set SRVPORT 1080
run -j
```

---

## 2. Configuração e Uso do ProxyChains

Configure `/etc/proxychains4.conf` ou `/etc/proxychains.conf` com a linha:

```text
socks4 127.0.0.1 1080
```

### Executar Ferramentas Através do Pivoting:
```bash
# Nmap via ProxyChains (usar obrigatoriamente -sT e -Pn)
proxychains nmap -sT -Pn -p 445,80,22,3389 10.10.20.5

# SMBClient via ProxyChains
proxychains smbclient -L //10.10.20.5 -N
```

---

## 3. Redirecionamento de Portas (Port Forwarding)

### Via Meterpreter
```bash
# Redireciona a porta 3389 local para a 3389 do alvo interno 10.10.20.5
portfwd add -l 3389 -p 3389 -r 10.10.20.5
```

### Via SSH Tunneling (Local Port Forwarding)
```bash
ssh -L 8080:10.10.20.5:80 usuario@IP_PIVOT
```