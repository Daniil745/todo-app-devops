# 🚀 Production-Ready DevOps Stack with 11 Containers

<div align="center">

[![Docker](https://img.shields.io/badge/Docker-24.x-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![Ubuntu](https://img.shields.io/badge/Ubuntu-24.04_LTS-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)](https://ubuntu.com/)
[![Prometheus](https://img.shields.io/badge/Prometheus-Monitoring-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)](https://prometheus.io/)
[![Grafana](https://img.shields.io/badge/Grafana-Dashboards-F46800?style=for-the-badge&logo=grafana&logoColor=white)](https://grafana.com/)
[![Ansible](https://img.shields.io/badge/Ansible-Automation-EE0000?style=for-the-badge&logo=ansible&logoColor=white)](https://www.ansible.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)

<h3>A comprehensive DevOps stack with full monitoring and automation</h3>

[Report Bug](https://github.com/Daniil745/todo-app-devops/issues) · [Request Feature](https://github.com/Daniil745/todo-app-devops/issues)

</div>

## 📋 Overview

![image alt](https://github.com/Daniil745/todo-app-devops/blob/68a33befac323f25527c2ee06d17a21eeebc68e0/screenshots/architecture.png)

This project demonstrates a **production-ready DevOps stack** deployed on VirtualBox, consisting of **11 containers**, **2 PostgreSQL databases**, and **full monitoring** capabilities. It showcases best practices in containerization, orchestration, monitoring, and automation.

### Architecture Highlights
- 🐳 11 containers in a unified Docker network
- 🗄️ Dual PostgreSQL databases (Tasks + Logs)
- 📊 Comprehensive monitoring stack
- 🔧 Automated deployment with Ansible
- 🚀 Load-tested and production-ready

## 🏗️ Technology Stack

### Base Infrastructure

| Technology | Version | Purpose |
|------------|---------|---------|
| VirtualBox | 7.x | Hypervisor for VM |
| Ubuntu | 24.04 LTS | Server OS |
| Docker | 24.x | Containerization |
| Docker Compose | 2.x | Container orchestration |

### Applications

| Component | Purpose | Port |
|-----------|---------|------|
| Flask App | Todo application | 5001 |
| PostgreSQL (Tasks) | Main database | 5432 |
| PostgreSQL (Logs) | Logs database | 5433 |
| Nginx | Reverse proxy | 8080 |

### Monitoring Stack

| Component | Purpose | Port |
|-----------|---------|------|
| Prometheus | Metrics collection | 9090 |
| Grafana | Data visualization | 3000 |
| cAdvisor | Container metrics | 8081 |
| Node Exporter | Server metrics | 9100 |
| PG Exporter (Tasks) | Tasks DB metrics | 9187 |
| PG Exporter (Logs) | Logs DB metrics | 9188 |

### Management Tools

| Component | Purpose | Port |
|-----------|---------|------|
| Portainer | Docker management | 9000 |
| Ansible | Deployment automation | - |

## 📁 Project Structure

```
todo-app-devops/
├── .gitignore
├── README.md
├── docker-compose.yml
├── inventory.example.ini
├── app/
│   ├── Dockerfile
│   ├── app.py
│   ├── requirements.txt
│   └── templates/
│       ├── index.html
│       └── logs.html
├── nginx/
│   ├── nginx.conf
│   └── default.conf
├── prometheus/
│   └── prometheus.yml
├── grafana/
│   └── grafana.yml
└── ansible/
    └── deploy.yml
```

## 🚀 Quick Start

### Prerequisites
- VirtualBox 7.x
- Ubuntu 24.04 LTS VM
- Docker and Docker Compose installed

### Installation Steps

**1️⃣ Clone the repository**
```bash
git clone https://github.com/Daniil745/todo-app-devops.git
cd todo-app-devops
```

**2️⃣ Configure environment**
```bash
# Create .env file from example
cp .env.example .env
# Edit with your parameters
nano .env
```

**3️⃣ Launch the stack**
```bash
docker compose up -d
```

**4️⃣ Verify deployment**
```bash
docker ps
# You should see 11 running containers
```

## 🌐 Service Access Points

| Service | URL | Credentials |
|---------|-----|-------------|
| Todo App | `http://your-ip-address:5001` | - |
| Grafana | `http://your-ip-address:3000` | admin/admin |
| Prometheus | `http://your-ip-address:9090` | - |
| Portainer | `http://your-ip-address:9000` | First login setup |
| cAdvisor | `http://your-ip-address:8081` | - |

## ⚙️ Ansible Deployment

### Automated Deployment

**1️⃣ Configure inventory**
```bash
cd ansible-todo
cp inventory.example.ini inventory.ini
# Edit inventory.ini with your SSH key path
nano inventory.ini
```

**2️⃣ Run deployment**
```bash
# Dry run (check mode)
ansible-playbook -i inventory.ini deploy.yml --check --ask-become-pass

# Actual deployment
ansible-playbook -i inventory.ini deploy.yml --ask-become-pass
```

## 📊 Monitoring Dashboards

- Node Exporter Dashboard: ![image alt](https://github.com/Daniil745/todo-app-devops/blob/68a33befac323f25527c2ee06d17a21eeebc68e0/screenshots/node%20exporter%20first%20dashboard.png)
- PostgreSQL Dashboard:
![image alt](https://github.com/Daniil745/todo-app-devops/blob/68a33befac323f25527c2ee06d17a21eeebc68e0/screenshots/node%20exporter%20second%20dashboard.png)

## 🏋️ Load Testing Results

### Test Configuration
- **Tool**: [hey](https://github.com/rakyll/hey)
- **Target**: Main application page
- **Method**: GET requests

### Iteration 1: 1,000 requests with 10 concurrency

---

![image alt](https://github.com/Daniil745/todo-app-devops/blob/68a33befac323f25527c2ee06d17a21eeebc68e0/screenshots/first%20testing.png)

---

| Metric | Value | Rating |
|--------|-------|--------|
| Requests/sec | 134 RPS | ⭐ Excellent |
| Avg Response Time | 65 ms | ⭐ Excellent |
| Slowest Request | 1.15 s | ⚡ Average |
| Errors | 0% | ⭐ Excellent |

### Iteration 2: 5,000 requests with 50 concurrency

---

![image alt](https://github.com/Daniil745/todo-app-devops/blob/68a33befac323f25527c2ee06d17a21eeebc68e0/screenshots/second%20testing.png)

---

| Metric | Value | Rating |
|--------|-------|--------|
| Requests/sec | 196 RPS | ⭐ Excellent |
| Avg Response Time | 232 ms | ⚡ Average |
| Slowest Request | 1.80 s | ⚡ Average |
| Errors | 0% | ⭐ Excellent |

### Iteration 3: 10,000 requests with 100 concurrency

---

![image alt](https://github.com/Daniil745/todo-app-devops/blob/68a33befac323f25527c2ee06d17a21eeebc68e0/screenshots/third%20testing.png)

---

| Metric | Value | Rating |
|--------|-------|--------|
| Requests/sec | 371 RPS | ⭐ Excellent |
| Avg Response Time | 254 ms | ⚡ Average |
| Slowest Request | 2.73 s | ⚡ Average |
| Errors | 0% | ⭐ Excellent |

## 📈 Performance Analysis

### Key Findings

**1. Throughput Dynamics**
- Linear growth in throughput with increased concurrency
- Efficient resource utilization and scaling capabilities
- Peak performance of 371 RPS under maximum load

**2. Response Time Analysis**
- 3.5-4x increase in response time at higher concurrency
- Indicates queue formation and potential database bottlenecks
- Still within acceptable limits for average responses

**3. Reliability**
- **0% error rate** across all test scenarios
- System handled 10,000 requests without failures
- Confirms robust concurrent connection handling

### Recommendations for Optimization
- Implement connection pooling for PostgreSQL
- Add caching layer (Redis/Memcached)
- Optimize database queries and indexes
- Consider horizontal scaling for high-load scenarios

## 🛡️ Security Features

- 🔐 SSH key authentication (no passwords)
- 🔥 UFW firewall with minimal open ports
- 👤 Non-root users in containers
- 📝 .gitignore for secrets and sensitive data
- 🔒 Secure environment variable management

## 📱 Application Screenshots

- Desktop View:

---

![image alt](https://github.com/Daniil745/todo-app-devops/blob/68a33befac323f25527c2ee06d17a21eeebc68e0/screenshots/first%20pc%20screen.png)

---

![image alt](https://github.com/Daniil745/todo-app-devops/blob/68a33befac323f25527c2ee06d17a21eeebc68e0/screenshots/second%20pc%20screen.png)

---

- Mobile View:

---

![image alt](https://github.com/Daniil745/todo-app-devops/blob/68a33befac323f25527c2ee06d17a21eeebc68e0/screenshots/first%20screen%20mobile.jpg)

---

![image alt](https://github.com/Daniil745/todo-app-devops/blob/68a33befac323f25527c2ee06d17a21eeebc68e0/screenshots/second%20screen%20mobile.jpg)

---

## ✨ Key Achievements

- ✅ 11 interconnected containers in unified network
- ✅ Dual PostgreSQL databases with dedicated purposes
- ✅ Full-stack monitoring with custom dashboards
- ✅ Automated deployment with Ansible
- ✅ Comprehensive load testing and analysis
- ✅ Responsive web design for all devices
- ✅ Security best practices implemented

## 🛠️ Built With

- [Flask](https://flask.palletsprojects.com/) - Web framework
- [PostgreSQL](https://www.postgresql.org/) - Database
- [Nginx](https://nginx.org/) - Reverse proxy
- [Prometheus](https://prometheus.io/) - Metrics collection
- [Grafana](https://grafana.com/) - Visualization
- [Docker](https://www.docker.com/) - Containerization
- [Ansible](https://www.ansible.com/) - Automation
- [Portainer](https://www.portainer.io/) - Docker management

## 👨‍💻 Author

**Daniil**
- GitHub: [@Daniil745](https://github.com/Daniil745)
- Project Link: [https://github.com/Daniil745/todo-app-devops](https://github.com/Daniil745/todo-app-devops)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<div align="center">
  <sub>If you found this project helpful, please give it a ⭐!</sub>
  <br>
  <sub>Built with ❤️ for the DevOps community</sub>
</div>

