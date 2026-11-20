# 🌐 NGINX Edge Gateway (`nginx-proxy`)

![NGINX](https://img.shields.io/badge/NGINX-1.26--alpine-009639?style=for-the-badge&logo=nginx&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Cloudflare](https://img.shields.io/badge/Cloudflare-Origin%20CA-F38020?style=for-the-badge&logo=cloudflare&logoColor=white)
![TLS](https://img.shields.io/badge/SSL%2FTLS-1.2%20%2F%201.3%20Full%20Strict-10B981?style=for-the-badge&logo=letsencrypt&logoColor=white)

Proxy reverso de borda responsável pela terminação **SSL/TLS (Cloudflare Origin CA)**, redirecionamento forçado `HTTP → HTTPS` e roteamento via Virtual Hosts isolados para todos os microsserviços do **GomesLab** através da rede Docker externa `webnet`.

---

## 🔀 Fluxo de Tráfego & Arquitetura

```text
🌍 Internet (HTTPS :443)
      │
      ▼
☁️ Cloudflare Edge (Proxy / WAF / CDN)
      │  [Criptografia End-to-End: Full Strict]
      ▼
🛡️ OCI VCN & Firewall (Porta 80 / 443)
      │
      ▼
🌐 NGINX Reverse Proxy (nginx:1.26-alpine)
      ├──► 🏠 gomeslab.com.br           ──► Landing Page Estática (/usr/share/nginx/html)
      ├──► 🔐 vault.gomeslab.com.br     ──► http://vaultwarden:80
      ├──► 🐳 portainer.gomeslab.com.br ──► http://portainer:9000
      ├──► 📡 uptime.gomeslab.com.br    ──► http://uptime-kuma:3001
      ├──► 📊 grafana.gomeslab.com.br   ──► http://grafana:3000
      └──► 🧰 tools.gomeslab.com.br     ──► http://it-tools:80

nginx-proxy/
├── 📄 docker-compose.yaml   # Orquestração do contêiner com limites de RAM (64M) e CPU (0.25)
├── 📁 conf.d/               # Virtual Hosts dedicados por subdomínio
│   ├── default.conf         # Portal principal (gomeslab.com.br e www) + redirect HTTP -> HTTPS
│   ├── vault.conf           # Proxy reverso para o Vaultwarden (com suporte a WebSockets)
│   ├── portainer.conf       # Proxy reverso para o Portainer CE
│   ├── uptime.conf          # Proxy reverso para o Uptime Kuma
│   ├── grafana.conf         # Proxy reverso para o Grafana OSS
│   └── tools.conf           # Proxy reverso para a suíte IT-Tools
├── 📁 html/
│   └── index.html           # Landing Page institucional estática (zero consumo extra de RAM)
└── 🔒 certs/                # [IGNORADO NO GIT] Certificados origin.pem e origin.key
