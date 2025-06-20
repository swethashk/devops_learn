######  Kubernetes Manifest Files

Kubernetes manifest files are YAML (or JSON) configuration files used to define the **desired state** of objects in a Kubernetes cluster—such as pods, deployments, services, and more.

These files tell Kubernetes **what resources to create and manage**, and **how** they should behave.

---

###### Common Kubernetes Resource Types

| Resource     | Description |
|--------------|-------------|
| `Pod`        | Defines a single or multiple containers |
| `Deployment` | Manages pod replicas and rolling updates |
| `Service`    | Exposes applications via networking |
| `ConfigMap`  | Stores non-sensitive configuration data |
| `Secret`     | Stores sensitive data like passwords and tokens |
| `Ingress`    | Manages external HTTP/S access |
| `Namespace`  | Provides logical separation of resources |

---

######  Sample Deployment Manifest

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp-container
        image: nginx
        ports:
        - containerPort: 80
