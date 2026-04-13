# 🚀 Cloud-Native Banking Platform (Kubernetes)

A full **cloud-native banking system** deployed on a **3-node Kubernetes cluster (Minikube)** using Docker, Node.js, NGINX, and PostgreSQL.

This project demonstrates real-world **DevOps & Kubernetes practices** including container orchestration, scaling, networking, and debugging distributed systems.

---

## 🏗️ Architecture

User → Ingress → Frontend → Backend → PostgreSQL

---

## ⚙️ Tech Stack

- Kubernetes (Minikube - 3 Nodes)
- Docker
- Node.js / Express
- NGINX
- PostgreSQL

---

## 🚀 Features

- Create bank accounts
- View balances
- Transfer money
- Track transactions

---

## ☸️ Kubernetes Concepts Used

- Deployments
- StatefulSet (PostgreSQL)
- Services (ClusterIP)
- Ingress Controller
- ConfigMaps & Secrets
- HPA (Horizontal Pod Autoscaler)

---

## ⚠️ Challenges Solved

- Pod scheduling issues
- PVC binding problems
- Ingress routing errors
- Multi-node cluster debugging
- Service communication issues

---

## 🛠️ How to Run

```bash
minikube start --nodes 3 --cpus 4 --memory 8192 --driver=docker
minikube addons enable ingress
docker build -t banking-api:v1 app/backend
docker build -t banking-dashboard:v1 app/frontend
minikube image load banking-api:v1
minikube image load banking-dashboard:v1
kubectl apply -f k8s/
Project Structure

📁 Project Structure
     banking-platform-k8s/
        app/
        k8s/
        README.md
👩‍💻 Author
Mariam Mansour
DevOps Engineer | Kubernetes & Cloud Enthusiast