# 🧰 IT-Tools (`it-tools`)

![IT-Tools](https://img.shields.io/badge/IT--Tools-2024.10.22--7ca5933-10B981?style=for-the-badge&logo=toolbox&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Architecture](https://img.shields.io/badge/Mode-Stateless%20Client--Side-6366F1?style=for-the-badge&logo=javascript&logoColor=white)

Suíte web de utilitários para administradores de sistemas, engenheiros de redes e desenvolvedores do **GomesLab** (calculadora de sub-redes IPv4/CIDR, gerador de hashes e senhas, conversores Base64/JSON/YAML, parsers JWT e ferramentas de criptografia), executando processamento 100% local no navegador do cliente (*zero data retention*).

---

## 🏗️ Integração & Arquitetura

```text
🌐 NGINX Edge Gateway (tools.gomeslab.com.br)
       │
       ▼ [Rede Externa: webnet]
🧰 IT-Tools (it-tools:80) ──► Entrega SPA estática (Vue.js / NGINX interno)

it-tools/
├── 📄 docker-compose.yaml   # Orquestração stateless do IT-Tools com limite de 64M RAM
└── 📄 README.md             # Documentação do serviço
