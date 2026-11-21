# 📊 Grafana OSS (`grafana`)

![Grafana](https://img.shields.io/badge/Grafana%20OSS-11.6.0-F46800?style=for-the-badge&logo=grafana&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![SQLite](https://img.shields.io/badge/Storage-SQLite%20Embedded-003B57?style=for-the-badge&logo=sqlite&logoColor=white)
![Optimization](https://img.shields.io/badge/Go%20Runtime-GOGC%3D50-00ADD8?style=for-the-badge&logo=go&logoColor=white)

Plataforma de observabilidade, visualização de métricas e análise de dashboards do **GomesLab**, ajustada com otimização agressiva do *Garbage Collector* da linguagem Go (`GOGC=50`) para operar com estabilidade em instâncias de memória restrita (**OCI Always Free**).

---

## 🏗️ Integração & Arquitetura

```text
🌐 NGINX Edge Gateway (grafana.gomeslab.com.br)
       │
       ▼ [Rede Externa: webnet]
📊 Grafana OSS (grafana:3000)
       ├──► 🗄️ Banco Interno SQLite (/var/lib/grafana/grafana.db)
       └──► 🔌 Data Sources (Prometheus / Zabbix / InfluxDB / APIs)

grafana/
├── 📄 docker-compose.yaml   # Orquestração do Grafana OSS com limite de 192M RAM e GOGC=50
├── 📄 README.md             # Documentação do serviço
└── 🔒 data/                 # [IGNORADO NO GIT] Banco grafana.db, plugins, sessões e chaves
