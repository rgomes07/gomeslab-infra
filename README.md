# 🏗️ GomesLab Infrastructure (`gomeslab-infra`)

[![Deploy GomesLab Infrastructure](https://github.com/rgomes07/gomeslab-infra/actions/workflows/deploy.yml/badge.svg)](https://github.com/rgomes07/gomeslab-infra/actions/workflows/deploy.yml)
![OCI Always Free](https://img.shields.io/badge/Cloud-OCI%20Always%20Free-F80000?style=flat-square&logo=oracle&logoColor=white)
![Ubuntu 24.04](https://img.shields.io/badge/OS-Ubuntu%2024.04%20LTS-E95420?style=flat-square&logo=ubuntu&logoColor=white)
![Docker Compose](https://img.shields.io/badge/Runtime-Docker%20Compose-2496ED?style=flat-square&logo=docker&logoColor=white)
![GitOps](https://img.shields.io/badge/Workflow-GitOps%20%2F%20CI--CD-2088FF?style=flat-square&logo=githubactions&logoColor=white)

Repositório centralizado de **Infrastructure as Code (IaC)** do ambiente self-hosted **GomesLab**, hospedado em uma instância **Oracle Cloud Infrastructure (OCI)** (`VM.Standard.E2.1.Micro` — 1 OCPU, 1 GB RAM + 2 GB Swap) operando sob práticas **GitOps** com validação e entrega contínua automatizadas via **GitHub Actions**.

---

## 🔄 Fluxo GitOps & Pipeline CI/CD

Toda alteração na infraestrutura segue o fluxo declarativo versionado no Git, eliminando alterações manuais não rastreadas (*configuration drift*) em produção:

```text
💻 Commit / Push (main)
       │
       ▼
🔍 Job 1: Quality Gate (GitHub Runner)
       ├── Checkout do código (actions/checkout@v4)
       └── Validação estática de sintaxe (docker compose config -q)
       │
       ▼ (Somente se 100% válido)
🚀 Job 2: Smart Deploy via SSH (VM OCI)
       ├── Sincronização limpa (git fetch + git reset --hard origin/main)
       ├── Detecção de impacto por diretório (git diff --name-only)
       ├── Se nginx/ mudou ──► nginx -t && nginx -s reload
       └── Se <stack>/ mudou ──► docker compose up -d --remove-orphans

gomeslab-infra/
├── 📁 .github/
│   └── 📁 workflows/
│       └── 📄 deploy.yml          # Pipeline CI/CD (Validação YAML + Smart Deploy SSH)
├── 📁 grafana/                    # Visualização de métricas e dashboards (OSS 11.6.0)
├── 📁 it-tools/                   # Utilitários web para desenvolvedores e SysAdmins
├── 📁 monitoring/                 # Coleta de métricas do host (Prometheus + Node Exporter)
├── 📁 nginx/                      # Reverse Proxy, Virtual Hosts, SSL Cloudflare e Rate Limiting
├── 📁 portainer/                  # Gerenciamento visual de contêineres e redes (CE 2.27.3)
├── 📁 uptime-kuma/                # Monitoramento de disponibilidade e status HTTP/TCP
├── 📁 vaultwarden/                # Cofre de senhas self-hosted + PostgreSQL 16 Alpine
├── 📄 .gitignore                  # Regras de exclusão de dados sensíveis e volumes persistentes
└── 📄 README.md                   # Documentação principal da arquitetura

👨💻 Autor
Ricardo Gomes — Systems Administrator & Hosting Analyst

🔗 Portal GomesLab • GitHub (@rgomes07)
