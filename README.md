## 🚀 Acesso ao Laboratório

📂 **Repositório completo no GitHub**
- Contém o código, logs e outputs utilizados no projeto.

📓 **Abrir notebook no Google Colab**
- Permite executar o código diretamente no navegador.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://github.com/joaodalfovo/Python-log-analysis/blob/2c05e695afb952a1682fda9daf9b4f005bc995d5/HomeLabLogPython.ipynb)

📁 **Acessar pasta completa no Google Drive**
- Contém o ambiente original do laboratório com os arquivos utilizados.

🔗 (https://drive.google.com/drive/folders/154cj35EObw_UpY5gBqviLVq5ITLwvNf1?usp=drive_link)

## Home Lab – Análise de Logs de Segurança com Python

Detecção de Brute Force SSH, Web Scanning (404) e Uso de Comandos Privilegiados

### 📄 Descrição do Projeto

Este repositório documenta um home lab de análise de logs de segurança utilizando Python, com foco na identificação de atividades suspeitas em servidores Linux e serviços web.

O laboratório simula diferentes tipos de eventos de segurança, incluindo tentativas de brute force SSH, scans em aplicações web detectados por erros HTTP 404, e execução de comandos privilegiados via sudo.

Um parser em Python foi desenvolvido para processar os logs, extrair eventos relevantes e gerar um resumo analítico com indicadores de segurança, permitindo identificar rapidamente possíveis comportamentos maliciosos.

O objetivo é demonstrar como logs brutos podem ser transformados em inteligência de segurança, desenvolvendo habilidades de detecção, correlação e análise de eventos utilizadas em ambientes SOC (Security Operations Center).

---

## 🎯 Objetivo do Laboratório

Identificar tentativas de brute force em SSH

Detectar scans em aplicações web através de erros HTTP 404

Analisar comandos executados com privilégios elevados (sudo)

Correlacionar falhas de login com logins bem-sucedidos

Classificar IPs suspeitos com base em comportamento

Gerar um resumo analítico automatizado dos eventos de segurança

Desenvolver raciocínio analítico aplicado a SOC / Blue Team

## 🛠️ Ambiente Utilizado

Linguagem: Python

Ambiente de execução: Google Colab

Fonte de Logs: Sample.log

Armazenamento de dados: Google Drive

<img width="509" height="308" alt="image" src="https://github.com/user-attachments/assets/b9ba521c-aff8-4f35-96ef-d46981babea6" />

Tecnologias envolvidas:

Python

Regex (Regular Expressions)

Python Collections (Counter)

Log Parsing

Linux Authentication Logs

Web Server Logs

Security Event Analysis

## 🔎 Eventos de Segurança Simulados

O log utilizado no laboratório contém diferentes tipos de eventos de segurança.

Falhas de autenticação SSH

Simulação de ataques de brute force com múltiplas tentativas de login.

Exemplo:

sshd Failed password for invalid user admin from 203.44.10.55

Login SSH bem-sucedido

Permite correlacionar se um IP que tentou diversas falhas conseguiu acessar o sistema posteriormente.

sshd Accepted password for joao from 191.10.20.30

Execução de comandos com sudo

Detecta atividades realizadas com privilégios administrativos.

sudo user=admin command=/bin/cat /etc/shadow

Web Scanning (HTTP 404)

Detecta tentativas de acesso a endpoints sensíveis em aplicações web.

Exemplo de caminhos frequentemente buscados em scans automatizados:

/wp-login.php
/phpmyadmin
/.env
/config.php
/db.sql

Esses padrões são comuns em ferramentas automatizadas de reconnaissance e vulnerability scanning.

```
Sample.log
﻿2026-03-05 20:58:01 INFO sshd Failed password for invalid user admin from 191.10.20.30 port 50112
2026-03-05 20:58:02 INFO sshd Failed password for root from 191.10.20.30 port 50115
2026-03-05 20:58:04 INFO sshd Failed password for root from 191.10.20.30 port 50118
2026-03-05 20:58:06 INFO sshd Failed password for user from 191.10.20.30 port 50120
2026-03-05 20:58:08 INFO sshd Failed password for test from 191.10.20.30 port 50125
2026-03-05 20:58:11 INFO sshd Failed password for guest from 191.10.20.30 port 50128


2026-03-05 20:59:02 INFO sshd Failed password for root from 185.44.22.19 port 41233
2026-03-05 20:59:05 INFO sshd Failed password for root from 185.44.22.19 port 41236
2026-03-05 20:59:08 INFO sshd Failed password for root from 185.44.22.19 port 41239
2026-03-05 20:59:10 INFO sshd Failed password for root from 185.44.22.19 port 41242


2026-03-05 21:00:12 INFO sshd Accepted password for joao from 191.10.20.30 port 50140
2026-03-05 21:00:15 WARN sudo user=joao command=/usr/bin/apt update
2026-03-05 21:00:20 WARN sudo user=joao command=/usr/bin/apt upgrade


2026-03-05 21:01:02 INFO nginx 404 GET /wp-login.php from 45.67.89.10
2026-03-05 21:01:05 INFO nginx 404 GET /phpmyadmin from 45.67.89.10
2026-03-05 21:01:07 INFO nginx 404 GET /.env from 45.67.89.10
2026-03-05 21:01:09 INFO nginx 404 GET /admin from 45.67.89.10
2026-03-05 21:01:12 INFO nginx 404 GET /backup.zip from 45.67.89.10


2026-03-05 21:02:11 INFO nginx 200 GET /index.html from 177.55.201.18
2026-03-05 21:02:14 INFO nginx 200 GET /products from 177.55.201.18
2026-03-05 21:02:18 INFO nginx 200 GET /contact from 177.55.201.18


2026-03-05 21:03:02 INFO sshd Failed password for invalid user oracle from 203.44.10.55 port 49822
2026-03-05 21:03:04 INFO sshd Failed password for invalid user postgres from 203.44.10.55 port 49824
2026-03-05 21:03:07 INFO sshd Failed password for invalid user admin from 203.44.10.55 port 49827
2026-03-05 21:03:10 INFO sshd Failed password for invalid user ubuntu from 203.44.10.55 port 49830
2026-03-05 21:03:13 INFO sshd Failed password for invalid user test from 203.44.10.55 port 49833
2026-03-05 21:03:16 INFO sshd Failed password for invalid user pi from 203.44.10.55 port 49835


2026-03-05 21:04:02 WARN sudo user=admin command=/bin/cat /etc/shadow
2026-03-05 21:04:05 WARN sudo user=admin command=/usr/bin/nano /etc/passwd


2026-03-05 21:05:01 INFO nginx 404 GET /wp-admin from 91.200.13.77
2026-03-05 21:05:03 INFO nginx 404 GET /xmlrpc.php from 91.200.13.77
2026-03-05 21:05:06 INFO nginx 404 GET /wp-login.php from 91.200.13.77
2026-03-05 21:05:08 INFO nginx 404 GET /config.php from 91.200.13.77


2026-03-05 21:06:01 INFO sshd Failed password for invalid user admin from 88.22.11.90 port 51220
2026-03-05 21:06:03 INFO sshd Failed password for invalid user admin from 88.22.11.90 port 51225
2026-03-05 21:06:06 INFO sshd Failed password for invalid user admin from 88.22.11.90 port 51228
2026-03-05 21:06:09 INFO sshd Failed password for invalid user admin from 88.22.11.90 port 51232


2026-03-05 21:07:02 INFO nginx 200 GET /home from 189.101.77.54
2026-03-05 21:07:04 INFO nginx 200 GET /products from 189.101.77.54
2026-03-05 21:07:08 INFO nginx 200 GET /cart from 189.101.77.54


2026-03-05 21:08:01 INFO sshd Accepted password for dev from 177.55.201.18 port 60022
2026-03-05 21:08:03 WARN sudo user=dev command=/usr/bin/systemctl restart nginx


2026-03-05 21:09:11 INFO nginx 404 GET /admin/login from 45.67.89.10
2026-03-05 21:09:13 INFO nginx 404 GET /db.sql from 45.67.89.10
2026-03-05 21:09:16 INFO nginx 404 GET /backup.tar.gz from 45.67.89.10
```

## ⚙️ Funcionamento do Parser

O script desenvolvido realiza as seguintes etapas:

### 1️⃣ Lê o arquivo de log linha por linha

<img width="493" height="61" alt="image" src="https://github.com/user-attachments/assets/0502811b-f108-4c2e-921b-5fbc84eeab6d" />

### 2️⃣ Utiliza expressões regulares (Regex) para identificar padrões de eventos:

Falhas SSH

Logins bem-sucedidos

Erros HTTP 404

Comandos sudo

<img width="758" height="853" alt="image" src="https://github.com/user-attachments/assets/7e7a97b0-fe57-4626-aca6-d7cc6057cdf5" />

### 3️⃣ Armazena os eventos em estruturas de dados

<img width="525" height="393" alt="image" src="https://github.com/user-attachments/assets/1c269404-ce50-4b6c-801d-37dddc2bcb01" />

### 4️⃣ Conta ocorrências utilizando Python Counter

<img width="209" height="205" alt="image" src="https://github.com/user-attachments/assets/16470be8-caa3-4795-8063-be138800ca85" />

### 5️⃣ Identifica IPs suspeitos com base em número de falhas

<img width="794" height="665" alt="image" src="https://github.com/user-attachments/assets/6369a506-f4b2-4836-bfac-a6e13aa801f4" />

### 6️⃣ Classifica o risco do IP:

HIGH → múltiplas falhas seguidas de login bem-sucedido

MEDIUM → múltiplas falhas sem login bem-sucedido

### 7️⃣ Gera um manu interativo dos eventos

<img width="863" height="683" alt="image" src="https://github.com/user-attachments/assets/faad6e10-2a05-4772-853d-754e67842095" />

## 📊 Exemplo de Resultado da Análise

Resumo gerado pelo parser:
```
Total de eventos analisados: 45

Top Failed SSH IPs:
191.10.20.30 → 6
203.44.10.55 → 6
185.44.22.19 → 4
88.22.11.90 → 4

Top Web Scan IPs (404):
45.67.89.10 → 8
91.200.13.77 → 4

Top Endpoints Atacados:
/wp-login.php
/phpmyadmin
/.env
/config.php

IPs Suspeitos Detectados:
191.10.20.30 → HIGH
203.44.10.55 → MEDIUM
```

<img width="512" height="475" alt="image" src="https://github.com/user-attachments/assets/8f081a57-c51f-4dc9-b40e-6d90d4dc30c3" />

--- 

## 🚨 Principais Indicadores Detectados
Brute Force SSH

IPs realizando múltiplas tentativas de autenticação.

Possível Comprometimento

IP que apresentou várias falhas e posteriormente conseguiu autenticar.

Web Scanning

Ferramentas automatizadas tentando acessar endpoints comuns de exploração.

Atividades Privilegiadas

Execução de comandos administrativos via sudo.

## 📚 Habilidades Demonstradas

Análise de logs de segurança

Criação de parsers de logs em Python

Uso de expressões regulares para detecção de eventos

Identificação de padrões de ataque comuns

Correlação de eventos de segurança

Construção de mini pipeline de análise de eventos

Raciocínio analítico aplicado a Blue Team / SOC

## 📂 Estrutura do Repositório
```
Python-log-analysis
│
├── HomeLabLogPython.ipynb
├── Sample.log
├── output
│   ├── summary.json
│   └── summary.csv
└── README.md
```
## 🧠 Conclusão

Este laboratório demonstra como logs de sistemas podem ser analisados programaticamente para detectar atividades suspeitas, permitindo transformar dados brutos em informação útil para investigação de segurança.

Esse tipo de abordagem é amplamente utilizado em ambientes SOC, onde analistas precisam correlacionar grandes volumes de eventos para identificar indicadores de comprometimento e comportamento malicioso.
