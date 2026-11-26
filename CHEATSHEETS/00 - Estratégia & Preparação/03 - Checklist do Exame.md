# ✅ Checklist do Exame DCPT

Utilize esta lista de verificação passo a passo durante a realização da prova para garantir total cobertura dos alvos e coleta de evidências.

---

## 📋 Lista de Verificação Etapa por Etapa

- [ ] Estrutura de diretórios criada (`~/dcpt/...`)
- [ ] Session manager (`tmux`/`screen`) configurado para múltiplas telas
- [ ] Nmap Fase 1 (`-p-`) executado em todos os alvos da rede
- [ ] Nmap Fase 2 (Detecção detalhada) rodado nas portas abertas
- [ ] Enumeração Web (`gobuster`/`ffuf`) concluída em serviços HTTP/HTTPS
- [ ] Enumeração de serviços específicos finalizada (SMB, SNMP, SMTP, FTP, etc.)
- [ ] Teste de RCE via ping/Wireshark realizado antes da abertura de shell reversa
- [ ] Shell reversa capturada e estabilizada (`pty.spawn` / `stty`)
- [ ] Enumeração de PrivEsc rodada (`LinPEAS` / `WinPEAS`)
- [ ] Escalação de privilégios concluída (Acesso `root` ou `SYSTEM`)
- [ ] **Screenshots de TODAS as evidências** salvas (`id`, `hostname`, `ifconfig`, `flags`)
- [ ] Hashes coletados e processados para quebra
- [ ] Flags lidas via `/bin/bash -i` (NUNCA direto por injeção Web)
- [ ] Rascunho do relatório documentado
- [ ] **Enviar a flag somente após garantir todas as evidências salvas**