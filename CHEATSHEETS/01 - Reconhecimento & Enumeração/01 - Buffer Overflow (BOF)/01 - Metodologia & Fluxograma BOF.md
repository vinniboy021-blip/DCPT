# 🐞 Metodologia & Fluxograma Buffer Overflow (BOF)

A exploração de Buffer Overflow em aplicações x86/x64 segue uma sequência rígida e determinística de etapas.

---

## 🔄 Fluxograma de Ataque

```
FUZZING → OFFSET → CONTROLE EIP → BADCHARS → JUMP ESP → SHELLCODE → EXPLOIT
```

---

## 📌 Etapas Detalhadas

1. **Fuzzing:** Enviar buffers de tamanho crescente para identificar a quantidade de bytes necessária para causar o crash da aplicação.
2. **Offset:** Determinar a distância exata em bytes do início do buffer até o registrador **EIP** (Instruction Pointer).
3. **Controle EIP:** Confirmar o controle sobrescrevendo o EIP com um valor pré-definido (ex: `42424242` = `BBBB`).
4. **Bad Characters:** Identificar bytes corrompidos ou truncados pela aplicação que não podem estar no shellcode final.
5. **JMP ESP:** Encontrar um endereço de instrução `JMP ESP` em um módulo/DLL compilado sem proteções ASLR/SafeSEH.
6. **Shellcode:** Gerar o payload de shell reversa com o `msfvenom` removendo todos os badchars identificados.
7. **Exploit Final:** Montar a estrutura `[PADDING] + [JMP ESP] + [NOPS] + [SHELLCODE]` e obter a shell.