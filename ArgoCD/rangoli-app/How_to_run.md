# 🌸 Rangoli App with Minikube + Argo CD (Short Steps)

1. `minikube start --driver=docker`
2. `eval $(minikube docker-env)`
3. Create `index.html` with Rangoli message
4. Create `Dockerfile` and add `COPY index.html`
5. `docker build -t rangoli-app:v1 .`
6. Write `deployment.yaml` and `service.yaml` under `k8s/`
7. `kubectl apply -f k8s/`
8. `minikube service rangoli-service` → open URL
9. *(Optional)* Install Argo CD:  
   `kubectl create ns argocd && kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`
10. `kubectl port-forward svc/argocd-server -n argocd 8080:443`
11. Open `https://localhost:8080` → login using decoded password
12. Add app in Argo CD with Git repo + path = `k8s/`
13. Push changes to Git → Argo CD detects + syncs ✅

🎉 Done! Your Rangoli is live via GitOps!
