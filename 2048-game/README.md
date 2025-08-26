# 2048 Game on Kubernetes with Kind & NGINX Ingress

This repository demonstrates how to deploy the classic 2048 game on a local Kubernetes cluster using Kind (Kubernetes in Docker) and an NGINX Ingress Controller. The goal is to run the game locally and access it via http://localhost.

```bash
# Create namespace
kubectl create ns 2048-game

# Deploy the 2048 game
kubectl apply -f deployment.yml

# Create the service
kubectl apply -f service.yml

# Verify pods and service
kubectl get pods -n 2048-game
kubectl get svc -n 2048-game

# Install NGINX ingress controller
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml

# Verify ingress controller pod
kubectl get pods -n ingress-nginx -o wide

# Apply the ingress resource
kubectl apply -f ingress.yml

# Verify ingress is live
kubectl get ingress -n 2048-game
kubectl describe ingress ingress-2048 -n 2048-game

# Test the application
curl -I http://localhost
