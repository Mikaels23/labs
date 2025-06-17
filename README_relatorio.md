# 🔓 Pentest Report - WebDAV Exploração via Gobuster e Cadaver

## 🧪 Ambiente do Laboratório
- Máquina Atacante: Parrot OS (Linux)
- Máquina Alvo: Linux Exploitable 2 (IP: `192.168.143.5`)
- Rede: `192.168.143.0/24`

## 🛠️ Ferramentas Utilizadas
| Ferramenta   | Finalidade                                |
|--------------|--------------------------------------------|
| `nmap`       | Descoberta de portas e serviços            |
| `gobuster`   | Força bruta de diretórios no servidor web  |
| `cadaver`    | Cliente WebDAV para upload de arquivos     |
| `curl`       | Teste de comandos via web shell            |

## 🔍 Vulnerabilidade Encontrada: WebDAV sem autenticação
Permite:
- Listagem de arquivos
- Upload de arquivos maliciosos (shells, scripts)
- Execução de código no servidor

## 💣 Exploração
1. Conexão com WebDAV usando `cadaver`
2. Upload de shell PHP
3. Execução remota via navegador

## ⚠️ Riscos
- Execução remota de comandos (RCE)
- Comprometimento completo do sistema
- Upload de malwares/backdoors

## 🛡️ Prevenções
| Ação                         | Descrição                                              |
|------------------------------|----------------------------------------------------------|
| ❌ Desabilitar WebDAV        | Remover se não for necessário                          |
| 🔐 Autenticação no WebDAV    | Requerer autenticação forte                            |
| ⚙️ Restringir métodos HTTP   | Bloquear PUT, DELETE, PROPFIND                         |
| 🧱 Firewall                  | Restringir acesso ao diretório                         |
| 📜 Monitoramento e logs      | Auditar uploads e execuções anormais                  |

## 📝 Conclusão
WebDAV exposto resultou em execução remota de comandos com shell PHP. Fica claro o risco de manter serviços não utilizados e mal configurados.

## 🧠 Recomendações
- Hardening do servidor
- Revisão de permissões e diretórios expostos
- Desabilitar serviços desnecessários