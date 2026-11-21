# 📡 Uptime Kuma (`uptime-kuma`)

![Uptime Kuma](https://img.shields.io/badge/Uptime%20Kuma-1.23.16-5CDD8B?style=for-the-badge&logo=uptimekuma&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Telegram](https://img.shields.io/badge/Alertas-Telegram%20Bot-26A5E4?style=for-the-badge&logo=telegram&logoColor=white)

Plataforma self-hosted de monitoramento ativo de disponibilidade (HTTP/HTTPS, TCP, Ping e status de contêineres Docker) com notificações instantâneas via **Telegram** para todos os serviços do **GomesLab**.

---

## 🏗️ Integração & Monitoramento

```text
🌐 NGINX Edge Gateway (uptime.gomeslab.com.br)
       │
       ▼ [Rede Externa: webnet]
📡 Uptime Kuma (uptime-kuma:3001)
       ├──► 🔍 Probes Externos (HTTPS via Cloudflare: gomeslab.com.br e subdomínios)
       ├──► 🐳 Socket Docker (/var/run/docker.sock:ro) ──► Healthcheck de Contêineres
       └──► 📲 Telegram Bot API ──► Alertas críticos em tempo real

uptime-kuma/
├── 📄 docker-compose.yaml   # Orquestração do Uptime Kuma com limite de 160M RAM
├── 📄 README.md             # Documentação do serviço
└── 🔒 data/                 # [IGNORADO NO GIT] Banco SQLite (kuma.db), credenciais e tokens Telegram
