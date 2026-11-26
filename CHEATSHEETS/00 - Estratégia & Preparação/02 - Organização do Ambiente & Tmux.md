# 🛠️ Organização do Ambiente & Tmux

Uma boa organização de pastas e sessões de terminal durante a prova previne a perda de logs e evidências cruciais para o relatório final.

---

## 📁 Estrutura de Diretórios do Pentest

Execute o comando abaixo na sua máquina atacante logo no início do exame:

```bash
# Crie sua estrutura de diretórios padronizada
mkdir -p ~/dcpt/{nmap,gobuster,exploits,shells,screenshots,relatorio}
```

### Finalidade das Pastas
- `nmap/`: Arquivos de saída de varreduras (`-oA`)
- `gobuster/`: Resultados de bruteforce de diretórios e DNS
- `exploits/`: Scripts customizados e PoCs adaptados
- `shells/`: Web shells, executáveis e scripts de reverse shell
- `screenshots/`: Evidências visuais de acesso e obtenção de flags
- `relatorio/`: Rascunhos de anotações e compilação de achados

---

## 🖥️ Gerenciamento de Terminais com Tmux

Tenha uma janela/painel dedicado para cada máquina do ambiente.

```bash
# Iniciar nova sessão do tmux
tmux new -s dcpt
```

### Atalhos Essenciais do Tmux (`Ctrl+B`)

| Atalho | Ação |
|--------|------|
| `Ctrl+B` `C` | Criar nova janela |
| `Ctrl+B` `N` | Ir para a próxima janela |
| `Ctrl+B` `P` | Ir para a janela anterior |
| `Ctrl+B` `"` | Dividir painel horizontalmente |
| `Ctrl+B` `%` | Dividir painel verticalmente |
| `Ctrl+B` `D` | Desconectar da sessão (`detach`) |

```bash
# Reconectar à sessão existente
tmux attach -t dcpt
```