# Banking Platform on Kubernetes

A cloud‑native banking platform deployed on Kubernetes using Docker,
NGINX, Node.js, and PostgreSQL.

This project demonstrates how to deploy and manage a multi‑tier
application on Kubernetes while applying networking, security, scaling,
and container orchestration concepts.

------------------------------------------------------------------------

## Project Overview

This project implements a simple banking system that allows users to:

-   Create bank accounts
-   View account balances
-   Transfer money between accounts
-   Track transactions

The application is built with a **frontend dashboard**, a **backend
API**, and a **PostgreSQL database**, all deployed inside a Kubernetes
cluster.

------------------------------------------------------------------------

## Architecture

User (Browser) ↓ NGINX Ingress Controller ↓ Frontend Dashboard (NGINX) ↓
Backend API (Node.js / Express) ↓ PostgreSQL Database (StatefulSet)

The application runs inside a **Kubernetes cluster using Minikube**.

------------------------------------------------------------------------

## Technologies Used

### Containerization

-   Docker
-   Custom images for frontend and backend

### Backend

-   Node.js
-   Express.js

### Frontend

-   HTML Dashboard
-   NGINX reverse proxy

### Database

-   PostgreSQL

### Kubernetes

-   Minikube
-   NGINX Ingress Controller

------------------------------------------------------------------------

## Kubernetes Concepts Implemented

### Namespace

A dedicated namespace was created to isolate all application resources.

Example: banking namespace

------------------------------------------------------------------------

### Deployments

Deployments were used to manage stateless applications:

-   banking-api (Node.js backend)
-   banking-dashboard (NGINX frontend)

Benefits: - automatic pod management - rolling updates - easy scaling

------------------------------------------------------------------------

### StatefulSet

PostgreSQL runs as a **StatefulSet**:

postgres-db

StatefulSets provide: - stable network identity - persistent storage -
ordered startup and shutdown

------------------------------------------------------------------------

### Services (ClusterIP)

Services allow communication between pods:

-   banking-api-service
-   banking-dashboard
-   postgres-db

------------------------------------------------------------------------

### Ingress

NGINX Ingress exposes the application externally:

http://banking.local

Traffic flow:

Browser → Ingress → Dashboard → API → Database

------------------------------------------------------------------------

### Network Policies

Network policies were implemented to secure pod communication.

Default deny policy blocks all traffic except:

-   Ingress → Dashboard
-   Dashboard → API
-   API → PostgreSQL
-   DNS access

------------------------------------------------------------------------

### RBAC

Role Based Access Control was implemented using Service Accounts:

-   banking-api-sa
-   banking-dashboard-sa

------------------------------------------------------------------------

### ConfigMaps

Used for storing configuration such as:

-   NGINX configuration
-   application settings

------------------------------------------------------------------------

### Secrets

Secrets store sensitive data like:

database password

------------------------------------------------------------------------

### Horizontal Pod Autoscaler (HPA)

Automatically scales API pods based on CPU usage.

Example: banking-api-hpa

------------------------------------------------------------------------

### Vertical Pod Autoscaler (VPA)

Provides recommendations for optimal CPU and memory resources.

Example: postgres-db-vpa

------------------------------------------------------------------------

## Docker Images

Two custom Docker images were created:

Backend API: banking-api:v1

Frontend Dashboard: banking-dashboard:v1

Images were built locally and loaded into Minikube.

------------------------------------------------------------------------

## Project Structure

banking-platform-k8s/

app/ backend/ app.js package.json Dockerfile

frontend/ index.html nginx.conf Dockerfile

k8s/ namespace.yaml deployments.yaml services.yaml ingress.yaml
network-policy.yaml rbac.yaml hpa.yaml vpa.yaml

README.md

------------------------------------------------------------------------

## Running the Project

### Start Minikube

minikube start --nodes 3 --cpus 4 --memory 8192 --driver=docker

### Enable Addons

minikube addons enable ingress minikube addons enable metrics-server

### Build Images

Backend

docker build -t banking-api:v1 app/backend

Frontend

docker build -t banking-dashboard:v1 app/frontend

### Load Images into Minikube

minikube image load banking-api:v1 minikube image load
banking-dashboard:v1

### Deploy Kubernetes Resources

kubectl apply -f k8s/

------------------------------------------------------------------------

## Access the Application

Add to hosts file:

192.168.49.2 banking.local

Then open:

http://banking.local

------------------------------------------------------------------------

## Features

-   Create bank accounts
-   View balances
-   Transfer money
-   Track transaction history

------------------------------------------------------------------------

## Challenges Solved

During this project:

-   Debugged NetworkPolicy blocking API traffic
-   Fixed NGINX reverse proxy routing
-   Troubleshot Ingress routing
-   Managed Docker images inside Minikube
-   Debugged Kubernetes service communication

------------------------------------------------------------------------

## Future Improvements

-   CI/CD pipeline
-   Helm charts
-   Monitoring with Prometheus & Grafana
-   Deploying on AWS EKS

------------------------------------------------------------------------

## Author

Ibrahim Ashraf DevOps & Cloud Enthusiast
