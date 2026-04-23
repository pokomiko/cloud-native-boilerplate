# 🚀 Cloud-Native Boilerplate (FastAPI + Worker + Kubernetes) 

A production-ready cloud-native boilerplate that demonstrates how to build, containerize, and deploy scalable services using FastAPI, background workers, and Kubernetes.

---

## 🧠 Overview

This project showcases a modern backend architecture designed for scalability, reliability, and maintainability.

It consists of:

* **FastAPI Service** — Handles incoming HTTP requests
* **Worker Service** — Processes background and scheduled tasks
* **Docker** — Ensures consistent environments
* **Kubernetes** — Manages deployment, scaling, and resilience
* **CI/CD Pipeline** — Automates testing, building, and deployment

---

## 🏗️ Architecture

```text
User → Kubernetes Service → API Pods → Response
                              ↓
                          Worker Pods
                              ↓
                         Background Jobs

Prometheus ← /metrics (API)
```

### Key Concepts

* Stateless API for horizontal scaling
* Independent worker for async/background processing
* Kubernetes for orchestration and self-healing
* Observability via Prometheus metrics

---

## 📂 Project Structure

```bash
.
├── src/
│   ├── api.py              # FastAPI app
│   ├── worker.py           # Background worker
│   ├── test_api.py         # Tests
│   └── requirements.txt
│
├── k8s/                    # Kubernetes manifests
│   ├── deployment-api.yaml
│   ├── deployment-worker.yaml
│   ├── service.yaml
│   ├── configmap.yaml
│   ├── hpa.yaml
│   └── pdb.yaml
│
├── Dockerfile.api
├── Dockerfile.worker
└── .github/workflows/
```

---

## ⚙️ Features

* ✅ FastAPI-based REST API
* ✅ Background worker with configurable interval
* ✅ Docker multi-stage builds
* ✅ Kubernetes deployment with:

  * Auto-scaling (HPA)
  * Health checks (liveness/readiness)
  * Rolling updates (zero downtime)
* ✅ Prometheus metrics support
* ✅ CI/CD pipeline with security scanning

---

## 🔌 API Endpoints

| Endpoint   | Description        |
| ---------- | ------------------ |
| `/`        | Basic service info |
| `/health`  | Liveness probe     |
| `/ready`   | Readiness probe    |
| `/metrics` | Prometheus metrics |

---

## 🖥️ Local Development

### Requirements

* Python 3.11+
* Docker (optional)

---

### Setup

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r src/requirements.txt
```

---

### Run API

```bash
APP_ENV=DEV uvicorn src.api:app --host 0.0.0.0 --port 8000
```

---

### Run Worker

```bash
APP_ENV=DEV WORKER_INTERVAL_SECONDS=60 python src/worker.py
```

---

### Run Tests

```bash
PYTHONPATH=src pytest -q src/test_api.py
```

---

## 🐳 Docker Usage

### Build Images

```bash
docker build -f Dockerfile.api -t api:local .
docker build -f Dockerfile.worker -t worker:local .
```

---

### Run Containers

```bash
docker run -p 8000:8000 -e APP_ENV=DEV api:local
docker run -e APP_ENV=DEV worker:local
```

---

## ☸️ Kubernetes Deployment

### 1. Apply Config

```bash
kubectl apply -f k8s/configmap.yaml
```

### 2. Deploy Services

```bash
kubectl apply -f k8s/
```

---

### Useful Commands

```bash
kubectl get pods
kubectl get svc
kubectl logs -l app=agnos-api
```

---

## 📈 Scaling & Reliability

* Horizontal Pod Autoscaler (HPA)
* Self-healing (auto-restart pods)
* Rolling updates (no downtime)
* PodDisruptionBudget for availability
* Resource limits for stability

---

## 📊 Monitoring

* Metrics exposed at `/metrics`
* Compatible with Prometheus and Grafana

---

## 🔄 CI/CD Pipeline

Automated via GitHub Actions:

1. Linting (`flake8`)
2. Testing (`pytest`)
3. Dependency audit (`pip-audit`)
4. Docker build
5. Security scan (Trivy)
6. Push to registry
7. Deploy to Kubernetes

---

### Required Secret

```bash
KUBE_CONFIG_DATA=<base64 kubeconfig>
```

---

## 🔐 Security Practices

* Non-root containers
* Minimal base images
* Dependency vulnerability scanning
* Image security scanning
* Restricted container permissions

---

## 💡 Design Decisions

* **Stateless API** → Enables easy horizontal scaling
* **Separate Worker** → Prevents blocking API requests
* **Kubernetes-native** → Built for cloud environments
* **Environment-based config** → Flexible deployment

---

## 🎯 Use Cases

* Microservices backend
* Cloud-native learning projects
* Production-ready API template
* Interview/portfolio demonstration

---

## 📌 Summary

This project demonstrates how to design and deploy a scalable backend system using modern cloud-native practices, with clear separation of concerns, strong observability, and automated delivery pipelines.