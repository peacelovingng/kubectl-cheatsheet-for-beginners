# 🧭 Kubectl Comprehensive Guide for Beginners

## 🔹 1. What is `kubectl`?

`kubectl` is the **command-line tool** for Kubernetes.  
It lets you **deploy apps**, **inspect/manage cluster resources**, and **view logs** — it’s how you talk to the **Kubernetes API Server**.

---

## 🔹 2. Installation

### 🧑‍💻 macOS
```bash
brew install kubectl
````

### 💻 Linux

```bash
sudo apt-get update
sudo apt-get install -y kubectl
```

### 🪟 Windows

```bash
choco install kubernetes-cli
```

### ✅ Verify

```bash
kubectl version --client
```

---

## 🔹 3. Cluster Configuration

Check cluster info:

```bash
kubectl cluster-info
```

Switch context:

```bash
kubectl config get-contexts
kubectl config use-context <context-name>
```

---

## 🔹 4. Basic Syntax

```bash
kubectl [command] [type] [name] [flags]
```

Example:

```bash
kubectl get pods my-pod -n dev
```

---

## 🔹 5. Common Resource Types

| Resource        | Description                             |
| --------------- | --------------------------------------- |
| **pods**        | Smallest deployable unit — container(s) |
| **services**    | Expose Pods on a network                |
| **deployments** | Manage ReplicaSets & rolling updates    |
| **replicasets** | Ensure Pods count matches desired       |
| **namespaces**  | Logical cluster segmentation            |
| **configmaps**  | Non-sensitive config key-values         |
| **secrets**     | Sensitive (base64) data                 |
| **nodes**       | Physical/virtual machines               |
| **ingress**     | HTTP(S) routing into cluster            |

---

## 🔹 6. Common Commands

### 🧱 Get Info

```bash
kubectl get pods
kubectl get pods -A
kubectl get svc
kubectl get deploy
kubectl get nodes
```

### 🔍 Inspect

```bash
kubectl describe pod <pod-name>
kubectl describe deployment <deployment-name>
```

### 📜 Logs

```bash
kubectl logs <pod-name>
kubectl logs <pod-name> -c <container>
kubectl logs -f <pod-name>
```

### 🚀 Create

```bash
kubectl create deployment nginx --image=nginx
kubectl create namespace dev
```

### 📦 Apply YAML

```bash
kubectl apply -f deployment.yaml
```

### 💣 Delete

```bash
kubectl delete pod <pod-name>
kubectl delete -f deployment.yaml
```

---

## 🔹 7. YAML Example

**nginx-deployment.yaml**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:latest
          ports:
            - containerPort: 80
```

Apply:

```bash
kubectl apply -f nginx-deployment.yaml
```

---

## 🔹 8. Namespaces

```bash
kubectl get ns
kubectl create namespace dev
kubectl get pods -n dev
kubectl apply -f deploy.yaml -n dev
```

Switch namespace:

```bash
kubectl config set-context --current --namespace=dev
```

---

## 🔹 9. Scaling & Updating

Scale:

```bash
kubectl scale deploy nginx-deployment --replicas=5
```

Update:

```bash
kubectl set image deploy/nginx-deployment nginx=nginx:1.21
```

Rollback:

```bash
kubectl rollout undo deploy/nginx-deployment
```

---

## 🔹 10. Debugging

Pod status:

```bash
kubectl get pods -o wide
```

Describe:

```bash
kubectl describe pod <pod-name>
```

Exec shell:

```bash
kubectl exec -it <pod-name> -- /bin/bash
```

Events:

```bash
kubectl get events --sort-by=.metadata.creationTimestamp
```

---

## 🔹 11. Labels & Selectors

Add label:

```bash
kubectl label pod <pod-name> env=prod
```

Filter:

```bash
kubectl get pods -l env=prod
```

---

## 🔹 12. Output Formatting

```bash
kubectl get pods -o wide
kubectl get pods -o yaml
kubectl get pods -o json
kubectl get pods -o custom-columns=NAME:.metadata.name,STATUS:.status.phase
```

---

## 🔹 13. Port Forwarding & Proxy

Port-forward a Pod:

```bash
kubectl port-forward pod/<pod-name> 8080:80
```

Run API proxy:

```bash
kubectl proxy
```

---

## 🔹 14. Autocomplete

### Bash/Zsh

```bash
source <(kubectl completion bash)
```

Permanent:

```bash
echo "source <(kubectl completion bash)" >> ~/.bashrc
```

---

## 🔹 15. Shortcuts

| Command                   | Shortcut             | Meaning     |
| ------------------------- | -------------------- | ----------- |
| `kubectl get pods`        | `kubectl get po`     | pods        |
| `kubectl get services`    | `kubectl get svc`    | services    |
| `kubectl get namespaces`  | `kubectl get ns`     | namespaces  |
| `kubectl get deployments` | `kubectl get deploy` | deployments |

---

## 🔹 16. Aliases

Add to `~/.bashrc` or `~/.zshrc`:

```bash
alias k='kubectl'
alias kgp='kubectl get pods'
alias kgs='kubectl get svc'
alias kga='kubectl get all'
alias kaf='kubectl apply -f'
```

---

## 🔹 17. Practice Cluster (Minikube)

Start:

```bash
minikube start
kubectl get nodes
```

---

## 🔹 18. Quick Reference

| Action           | Command                                    |
| ---------------- | ------------------------------------------ |
| List all pods    | `kubectl get pods -A`                      |
| Describe pod     | `kubectl describe pod <name>`              |
| View logs        | `kubectl logs <name>`                      |
| Exec shell       | `kubectl exec -it <name> -- bash`          |
| Apply YAML       | `kubectl apply -f file.yaml`               |
| Delete resource  | `kubectl delete -f file.yaml`              |
| Scale deployment | `kubectl scale deploy <name> --replicas=3` |
| Rollback         | `kubectl rollout undo deploy/<name>`       |

---

## 🔹 19. Practice Lab

1. Create namespace
2. Deploy Nginx
3. Expose via Service
4. Scale replicas to 5
5. Update image
6. Roll back
7. View logs & exec into pod

---

## 🎯 20. Next Steps

* Learn **Kubernetes architecture**
* Understand **Pods, Deployments, Services**
* Write **YAML manifests**
* Explore **Helm**, **Kustomize**, **kubectl plugins**

---

🧩 **Tip:** Practice `kubectl` daily on Minikube or a test cluster — muscle memory is key!

```
