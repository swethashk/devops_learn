# 🔁 Rangoli App Restart Guide (Minikube + Argo CD)

Use this guide to **stop** and **restart** your local Minikube cluster, app, and Argo CD dashboard.

---

## Start and Stop Everything

```bash
# Stop the Minikube cluster
minikube stop

# Optional: Delete the cluster if you want a fresh start
# minikube delete

## Start Everything
minikube start --driver=docker
eval $(minikube docker-env)
docker build -t rangoli-app:v1 .        
kubectl apply -f k8s/                  
minikube service rangoli-service

## Access Argo CD Dashboard

kubectl port-forward svc/argocd-server -n argocd 8080:443
kubectl -n argocd get secret argocd-initial-admin-secret \
  -o jsonpath="{.data.password}" | base64 --decode && echo
