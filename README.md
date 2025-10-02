# Kubernetes Ingress Demo

This project demonstrates how to use **Kubernetes Ingress** to route traffic to multiple services. It includes three apps (`food`, `cafe`, `sports`) each with its own Deployment and Service, and a single Ingress routing traffic based on path.

---

## Folder Structure

k8s-ingress-demo/
├── ingress.yaml
├── cafe.yaml
├── food.yaml
├── sports.yaml
└── README.md

---

## Prerequisites

- Kubernetes cluster (Minikube or any cluster)
- NGINX Ingress Controller installed
- `kubectl` CLI installed
- (Optional) `curl` for testing endpoints

---

## Deployment Instructions

1. Deploy the individual apps & services:

```bash
kubectl apply -f cafe.yaml
kubectl apply -f food.yaml
kubectl apply -f sports.yaml

```bash
Deploy the Ingress:
kubectl apply -f ingress.yaml

Accessing the Apps
Option 1: Port-forward (works on local Minikube)

kubectl port-forward -n ingress-nginx svc/ingress-nginx-controller 8080:80
curl http://localhost:8080/food
curl http://localhost:8080/cafe
curl http://localhost:8080/sports

Option 2: Map a host (if using host: in Ingress)

Get Minikube IP:

minikube ip
Add a line to /etc/hosts (Linux) 

192.168.49.2 myapp.com

Access apps via:

curl http://myapp.com/food
curl http://myapp.com/cafe
curl http://myapp.com/sports


Notes
Each app uses hashicorp/http-echo to simulate a simple HTTP response.

Ports in Services map container ports (5678) to arbitrary service ports (1000, 2000, 3000) for demonstration purposes.

This project is intended for local development and learning purposes.
