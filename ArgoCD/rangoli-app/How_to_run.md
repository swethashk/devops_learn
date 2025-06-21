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



✅ Scenario 1: Git Change → Argo CD Syncs
📘 Git updated → Argo CD syncs → Rangoli updated in cluster.

❌ Scenario 2: Manual Change → Argo CD Fixes
💥 edit Pod changed manually → Argo CD detects drift → auto-sync restores correct Rangoli.





✅ Scenario 1: Git Update → Argo CD Deploys New Rangoli
🧓 Grandma updates the notebook (Git), and Argo Didi (Argo CD) updates the yard (Kubernetes).

Steps:

Update index.html with a new message.

Build a new Docker image (e.g., rangoli-app:v2).

Update image tag in deployment.yaml.

Commit & push to GitHub.

Argo CD auto-syncs or you click "Sync" — new Rangoli appears!

❌ Scenario 2: Manual Change in Cluster → Argo CD Detects & Fixes
👦 A naughty cousin spoils the Rangoli directly in the yard. Argo Didi catches it and restores it.

Steps:

Manually exec into pod:
kubectl exec -it <pod> -- /bin/sh

Change HTML:
echo "<h1>❌ Rangoli was spoiled!</h1>" > /usr/share/nginx/html/index.html

Visit app — broken message appears.

Argo CD shows "OutOfSync".

Click Sync, or auto-heal fixes it — original Rangoli is back!
