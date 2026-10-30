# Azure Kubernetes Service — Hands-on Labs

A hands-on learning project focused on Docker, Kubernetes, Azure Kubernetes Service (AKS), Terraform, and Azure DevOps.

This repository documents my practical exercises and implementations as I progress through the **Azure Kubernetes Service with Azure DevOps and Terraform** course by StackSimplify.

The goal is to build and progressively improve a containerized application, starting with Docker and local Kubernetes before moving to Azure infrastructure and CI/CD pipelines.

## Technologies

- Docker
- Kubernetes
- kind (Kubernetes IN Docker)
- kubectl
- Azure Kubernetes Service (AKS) — planned
- Terraform — planned
- Azure DevOps — planned

## Project Structure

```text
aks-kubernetes-labs/
├── lab01-nginx/
│   ├── Dockerfile
│   └── index.html
├── kubernetes/
│   ├── deployments/
│   │   └── nginx-deployment.yaml
│   └── services/
│       └── nginx-service.yml
└── README.md
```

## Lab 01 — Docker Fundamentals

Created a custom Nginx Docker image serving a simple HTML application.

```bash
cd lab01-nginx

docker build -t aks-learning-nginx:v1 .
docker run -d -p 8090:80 aks-learning-nginx:v1
```

The application is accessible at `http://localhost:8090`.

## Lab 02 — Kubernetes Imperative Commands

Created a local Kubernetes cluster using kind.

```bash
kind create cluster --name aks-learning
```

Loaded the custom Docker image into the cluster:

```bash
kind load docker-image aks-learning-nginx:v1 --name aks-learning
```

Practiced:

- Creating Pods and Deployments.
- Managing ReplicaSets.
- Testing Pod self-healing.
- Scaling Deployments.
- Exposing applications using ClusterIP Services.
- Understanding Labels and Selectors.

## Lab 03 — Kubernetes Declarative Configuration

Created Kubernetes YAML manifests for the Nginx Deployment and Service.

Deploy the application:

```bash
kubectl apply -f kubernetes/deployments/nginx-deployment.yaml
kubectl apply -f kubernetes/services/nginx-service.yml
```

Verify:

```bash
kubectl get deployments
kubectl get replicasets
kubectl get pods
kubectl get services
```

Access the application:

```bash
kubectl port-forward service/nginx-service 8092:80
```

Open `http://localhost:8092` in a browser.

The Deployment currently defines **4 replicas**.

## Upcoming Labs

Future exercises will cover Kubernetes ConfigMaps, Secrets, persistent storage, rolling updates, rollbacks, AKS infrastructure, Terraform, and Azure DevOps CI/CD.

## Course Reference

This project is inspired by the StackSimplify course **Azure Kubernetes Service with Azure DevOps and Terraform**.

Course repository: https://github.com/stacksimplify/azure-aks-kubernetes-masterclass

All hands-on implementations in this repository are maintained separately from the instructor's source repository.
