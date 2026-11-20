# 🔐 Vaultwarden & PostgreSQL (`vaultwarden`)

![Vaultwarden](https://img.shields.io/badge/Vaultwarden-1.35.4-175DDC?style=for-the-badge&logo=bitwarden&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16.6--alpine-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Security](https://img.shields.io/badge/Network-Isolated%20Bridge-10B981?style=for-the-badge&logo=shield&logoColor=white)

Instância self-hosted do **Vaultwarden** (servidor compatível com clientes Bitwarden) respaldada por banco de dados **PostgreSQL 16**, operando com isolamento de rede em dois níveis e limites rígidos de memória para a **OCI Always Free**.

---

## 🏗️ Topologia & Isolamento de Rede

```text
🌐 NGINX Edge Gateway (vault.gomeslab.com.br)
       │
       ▼ [Rede Externa: webnet]
🔐 Vaultwarden Server (vaultwarden:80)
       │
       ▼ [Rede Interna Isolada: vault_internal (internal: true)]
🗄️ PostgreSQL 16 (vaultwarden-db:5432) ──► Sem acesso à Internet ou ao Gateway

vaultwarden/
├── 📄 docker-compose.yaml   # Orquestração da aplicação e do banco com limites de cgroups
├── 📄 .env.example          # Modelo seguro das variáveis de ambiente necessárias
├── 📄 README.md             # Documentação do serviço
├── 🔒 .env                  # [IGNORADO NO GIT] Senhas reais, DATABASE_URL e ADMIN_TOKEN
├── 🔒 vw-data/              # [IGNORADO NO GIT] Anexos, chaves RSA e ícones em cache
└── 🔒 pgdata/               # [IGNORADO NO GIT] Arquivos físicos do banco PostgreSQL
