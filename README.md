🦞 OpenClaw — Personal AI Assistant + Ollama (Mistral / Devstral)
<p align="center"> <picture> <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/openclaw-logo-text-dark.png"> <img src="https://raw.githubusercontent.com/openclaw/openclaw/main/docs/assets/openclaw-logo-text.png" alt="OpenClaw" width="500"> </picture> </p> <p align="center"> <strong>EXFOLIATE! EXFOLIATE!</strong> </p> <p align="center"> <img src="https://img.shields.io/badge/AI-100%25%20Local-success?style=for-the-badge"> <img src="https://img.shields.io/badge/Ollama-Mistral%20%7C%20Devstral-blue?style=for-the-badge"> <img src="https://img.shields.io/badge/OpenAI-NOT%20REQUIRED-critical?style=for-the-badge"> <img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge"> </p>

OpenClaw (Clawdbot) é um assistente de IA pessoal que você executa no seu próprio computador, com controle total.
Este setup utiliza Ollama + Mistral/Devstral, rodando 100% local no Windows, sem OpenAI API Key, sem cloud, sem custo.

O Gateway é apenas o plano de controle — o produto é o assistente.

✨ Por que esse setup?

⚡ Respostas rápidas (local)

🔒 Zero envio de dados para terceiros

💸 Zero custo por token

🧠 Controle total do modelo

🖥️ Funciona offline (após download do modelo)

Se você quer um assistente local, persistente e sempre ligado, este é o caminho.

📋 Requisitos

Windows 10 ou 11

Node.js (LTS)

Git

PowerShell ou CMD

1️⃣ Instalar o Ollama (Windows)
📥 Download

👉 https://ollama.com/download/windows

Instale normalmente.

▶️ Verificação
ollama --version


O serviço sobe automaticamente em:

http://127.0.0.1:11434

2️⃣ Baixar os modelos locais
ollama pull mistral
ollama pull devstral


Verifique:

ollama list

3️⃣ Testar o modelo (sanidade)
ollama run mistral


ou

ollama run devstral


Se responder, o Ollama está pronto.

4️⃣ Instalar o Clawdbot (CLI)
npm install -g clawdbot


Verificar:

clawdbot --version

5️⃣ Onboarding inicial (Wizard)

Crie sua pasta de trabalho:

mkdir clawd
cd clawd


Execute:

clawdbot onboard

⚙️ Configurações importantes no wizard

Mode: local

Model/Auth provider: ollama

Base URL:

http://127.0.0.1:11434/v1


API type: openai-completions

API Key:

ollama-local


Valor fictício — não é OpenAI

Auth header: false

6️⃣ 🔥 PASSO CRÍTICO — Remover OpenAI e forçar 100% local
📍 Arquivo de configuração
C:\Users\SEU_USUARIO\.clawdbot\clawdbot.json

🛠️ Opção A — Editar o arquivo (RECOMENDADO)

Garanta que apenas Ollama esteja configurado:

{
  "providers": {
    "ollama": {
      "baseUrl": "http://127.0.0.1:11434/v1",
      "apiKey": "ollama-local",
      "api": "openai-completions",
      "authHeader": false,
      "models": [
        {
          "id": "devstral:latest",
          "name": "devstral:latest",
          "reasoning": false
        }
      ]
    }
  },
  "agents": {
    "defaults": {
      "model": {
        "primary": "ollama/devstral:latest"
      }
    }
  }
}


❌ Não deve existir:

OPENAI_API_KEY

provider openai

modelos openai/gpt-*

🛠️ Opção B — Setar via CLI
clawdbot config


Provider: ollama

Modelo padrão: ollama/devstral:latest

Remova OpenAI da lista de modelos

7️⃣ Conferir configuração ativa
clawdbot config show


Confirme:

Modelo padrão → ollama/*

Nenhuma referência a OpenAI

8️⃣ Iniciar o OpenClaw (Clawdbot)
clawdbot


ou

clawdbot start


Logs esperados:

[gateway] agent model: ollama/devstral:latest
[heartbeat] started
[gateway] listening on ws://127.0.0.1:18789

📂 Estrutura criada
~/.clawdbot/
 ├─ agents/
 │   └─ main/
 │      ├─ sessions/
 │      └─ heartbeat.json
 ├─ clawdbot.json
 └─ logs/


Logs de runtime:

\tmp\clawdbot\

⚠️ Observações Importantes

O agent main é recriado automaticamente

O apiKey do Ollama é fake

Nenhuma requisição sai da máquina

Funciona offline após o download do modelo

🧠 Resumo

✔️ OpenClaw local
✔️ Ollama + Mistral / Devstral
✔️ Sem OpenAI
✔️ Zero custo
✔️ Controle total
