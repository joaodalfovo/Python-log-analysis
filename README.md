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

<img width="914" height="869" alt="image" src="https://github.com/user-attachments/assets/5f850571-67a9-4ee3-8849-06dfaab343ae" />

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
