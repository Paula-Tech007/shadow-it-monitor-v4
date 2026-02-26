# 🔐 Shadow IT Monitor v4.0 – Enterprise Dynamic Policy Engine

Sistema automatizado de detecção de Shadow IT baseado em análise de e-mails, scoring dinâmico de risco e políticas corporativas configuráveis via Google Sheets.

Projeto desenvolvido com foco em arquitetura enterprise, governança e rastreabilidade total de eventos.

---

## 🎯 Objetivo

Detectar possíveis usos não autorizados de ferramentas SaaS (Shadow IT) a partir de e-mails recebidos, aplicando:

- 🔎 Scoring de risco dinâmico
- 📋 Whitelist e Blacklist configuráveis
- 🧠 Motor de análise baseado em indicadores
- 🗂 Persistência completa de eventos
- 🚨 Alertas automáticos para riscos elevados

---

## 🏗 Arquitetura

Gmail Trigger  
↓  
Normalize Fields  
↓  
Dynamic Policy Layer (Google Sheets)  
↓  
Risk Engine (Scoring Inteligente)  
↓  
Audit Log Persistence  
↓  
High Risk Filter  
↓  
Telegram Alert  

### 🔒 Princípios Arquiteturais

- Nenhum evento é perdido (persistência antes do filtro)
- Políticas dinâmicas (sem hardcode)
- Suporte a subdomínios
- Auditoria completa
- Estrutura escalável para SOC

---

## 🛠 Tecnologias Utilizadas

- n8n
- Gmail API
- Google Sheets API
- Telegram Bot API
- JavaScript (Risk Engine)
- ISO 8601 Timestamping

---

## 🧠 Risk Engine – Lógica de Scoring

### 1️⃣ Whitelist Dinâmica
Se domínio estiver na whitelist → Score = 0

### 2️⃣ Blacklist Dinâmica
Se domínio estiver na blacklist → Score = 100 (Critical)

### 3️⃣ Indicadores de Alto Risco

| Palavra-chave | Peso |
|--------------|------|
| api key      | 40   |
| billing      | 35   |
| payment      | 35   |
| admin        | 30   |

### 4️⃣ Indicadores de Médio Risco

| Palavra-chave | Peso |
|--------------|------|
| trial        | 20   |
| subscription | 15   |
| verify       | 10   |
| activate     | 15   |

### 5️⃣ Penalidades

- Domínio externo não corporativo: +15  
- Múltiplos indicadores detectados: +10  

---

## 📊 Classificação de Risco

| Score | Nível |
|-------|--------|
| 0     | Whitelisted |
| 30+   | Medium |
| 60+   | High |
| 80+   | Critical |
| 100   | Blacklist |

---

## 📁 Estrutura do Google Sheets

### Aba: `Whitelist`
Coluna A: domínios permitidos

### Aba: `Blacklist`
Coluna A: domínios proibidos

### Aba: `AuditLog`

| domain | subject | riskScore | riskLevel | indicatorsMatched | governanceTag | detectedAt |

---

## 🚨 Alertas Automáticos

Alertas são enviados via Telegram quando:

riskScore >= 60

Incluindo:

- Domínio
- Score
- Nível de risco
- Tag de governança
- Timestamp ISO

---

## 📈 Governança Implementada

- Dynamic Policy Control
- Audit Trail Completo
- Detecção baseada em comportamento
- Separação entre ingestão, processamento e notificação
- Estrutura pronta para evolução SaaS multi-tenant

---

## 🚀 Roadmap

- [ ] Reincidência automática por domínio  
- [ ] Score acumulado semanal  
- [ ] Dashboard executivo  
- [ ] Multi-tenant architecture  
- [ ] Exportação automática para PDF executivo  

---

## 🧩 Como Importar no n8n

1. Abra o n8n  
2. Clique em “Import Workflow”  
3. Cole o JSON do projeto  
4. Configure:
   - Credenciais Gmail
   - Credenciais Google Sheets
   - Credenciais Telegram
5. Atualize o `sheetId`
6. Ative o workflow  

---

## 👩‍💻 Autora

**Paula Sabino**
  
Automação | Segurança | Governança | n8n Architect  

🔗 LinkedIn:  
https://www.linkedin.com/in/paula-sabino-49830573/

💻 GitHub:  
https://github.com/Paula-Tech007



