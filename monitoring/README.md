# 📈 Stack de Telemetria & Métricas (`monitoring`)

![Prometheus](https://img.shields.io/badge/Prometheus-v3.2.1-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)
![Node Exporter](https://img.shields.io/badge/Node%20Exporter-v1.9.0-009639?style=for-the-badge&logo=linux&logoColor=white)
![cAdvisor](https://img.shields.io/badge/cAdvisor-v0.51.0-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Grafana](https://img.shields.io/badge/Data%20Source-Grafana%20OSS-F46800?style=for-the-badge&logo=grafana&logoColor=white)

Pipeline leve de coleta de métricas de infraestrutura (Host Ubuntu 24.04) e contêineres Docker para alimentar os dashboards do **Grafana OSS** no **GomesLab**, otimizada para baixo consumo de memória na **OCI Always Free**.

---

## 🏗️ Arquitetura de Coleta

```text
📊 Grafana OSS (grafana:3000)
       │ [PromQL via rede webnet]
       ▼
🔥 Prometheus (prometheus:9090) ──► Scrape: 30s | Retenção: 7d / 512MB
       ├──► 🖥️ Node Exporter (node-exporter:9100) ──► Métricas do Kernel/Host OCI
       └──► 🐳 cAdvisor (cadvisor:8080)           ──► Métricas por Contêiner Docker

monitoring/
├── 📄 docker-compose.yaml       # Orquestração dos coletores com limites estritos de cgroups
├── 📄 README.md                 # Documentação da stack de telemetria
├── 📁 prometheus/
│   └── 📄 prometheus.yml        # Configuração dos jobs de scrape (oci-host e docker-containers)
└── 🔒 prometheus-data/          # [IGNORADO NO GIT] Banco TSDB local do Prometheus
