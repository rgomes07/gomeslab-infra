# 🐳 Portainer CE (`portainer`)

![Portainer](https://img.shields.io/badge/Portainer%20CE-2.27.3--alpine-13BEF9?style=for-the-badge&logo=portainer&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Security](https://img.shields.io/badge/Docker%20Socket-Read--Only-10B981?style=for-the-badge&logo=shield&logoColor=white)

Interface web leve para gerenciamento, inspeção de logs, monitoramento de recursos e controle operacional dos contêineres, redes e volumes do **GomesLab**.

---

## 🏗️ Integração & Arquitetura

```text
🌐 NGINX Edge Gateway (portainer.gomeslab.com.br)
       │
       ▼ [Rede Externa: webnet]
🐳 Portainer CE (portainer:9000)
       │
       ▼ [Bind Mount: /var/run/docker.sock:ro]
⚙️ Docker Engine Host (Inspeção e Gerenciamento)

portainer/
├── 📄 docker-compose.yaml   # Orquestração do Portainer CE com limite de 128M RAM
├── 📄 README.md             # Documentação do serviço
└── 🔒 data/                 # [IGNORADO NO GIT] Banco interno BoltDB, usuários e chaves TLS
