# 🚀 GomesLab Infrastructure (`gomeslab-infra`)

![Oracle Cloud](https://img.shields.io/badge/Oracle%20Cloud-Always%20Free-F80000?style=for-the-badge&logo=oracle&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-24.04%20LTS-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![NGINX](https://img.shields.io/badge/NGINX-Edge%20Gateway-009639?style=for-the-badge&logo=nginx&logoColor=white)
![Cloudflare](https://img.shields.io/badge/Cloudflare-Full%20Strict%20SSL-F38020?style=for-the-badge&logo=cloudflare&logoColor=white)

Repositório **Infrastructure-as-Code (IaC)** da nuvem privada **GomesLab** (`gomeslab.com.br`), arquitetada para rodar em produção com alta segurança, isolamento de rede e consumo estrito de recursos em uma instância **OCI Always Free (`VM.Standard.E2.1.Micro` — 1 GB RAM + 2 GB Swap)**.

---

## 🏗️ Arquitetura Geral & Topologia

```text
🌍 Usuários / Internet
       │ (HTTPS :443)
       ▼
☁️ Cloudflare DNS + Proxy (WAF / DDoS Protection / CDN)
       │ (TLS 1.3 End-to-End - Origin CA Certificate)
       ▼
🛡️ OCI VCN Security List & Ubuntu UFW (Apenas 22, 80, 443 expostas)
       │
       ▼
🌐 NGINX Reverse Proxy (nginx-proxy) ──► [Rede Docker: webnet]
       ├──► 🏠 gomeslab.com.br           (Portal Institucional Estático)
       ├──► 🔐 vault.gomeslab.com.br     (Vaultwarden + PostgreSQL em rede isolada)
       ├──► 🐳 portainer.gomeslab.com.br (Portainer CE)
       ├──► 📡 uptime.gomeslab.com.br    (Uptime Kuma + Alertas Telegram)
       ├──► 📊 grafana.gomeslab.com.br   (Grafana OSS)
       └──► 🧰 tools.gomeslab.com.br     (IT-Tools DevOps Suite)

gomeslab-infra/
├── 📄 .gitignore          # Bloqueio estrito de .env, certificados, chaves e volumes
├── 📄 LICENSE             # Licença MIT
├── 📄 README.md           # Documentação central da infraestrutura
├── 📁 nginx-proxy/        # Edge Reverse Proxy, Virtual Hosts e Landing Page
├── 📁 vaultwarden/        # [Em breve] Gerenciador de senhas + PostgreSQL
├── 📁 portainer/          # [Em breve] Orquestração visual Docker
├── 📁 uptime-kuma/        # [Em breve] Monitoramento e alertas
├── 📁 grafana/            # [Em breve] Dashboards e métricas
└── 📁 it-tools/           # [Em breve] Ferramentas DevOps

👨💻 Autor
Ricardo Gomes — Systems Administrator & Hosting Analyst

🔗 Portal GomesLab • GitHub (@rgomes07)
