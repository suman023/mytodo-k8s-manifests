# MyToDo K8s Manifests

Kubernetes manifests for MyToDo app. Managed by ArgoCD (GitOps).

## Files
```
mytodo-k8s-manifests/
├── 01-namespace.yaml      # mytodo namespace
├── 02-secret.yaml         # MySQL credentials
├── 03-configmap.yaml      # MySQL init script
├── 04-mysql.yaml          # MySQL StatefulSet + Service
├── 05-flask.yaml          # Flask Deployment + Service
└── argocd-app.yaml        # ArgoCD Application
```

## How it works
1. Jenkins updates image tag in `05-flask.yaml`
2. ArgoCD detects the change
3. ArgoCD auto-deploys to Minikube

## Deploy Manually
```bash
kubectl apply -f 01-namespace.yaml
kubectl apply -f 02-secret.yaml
kubectl apply -f 03-configmap.yaml
kubectl apply -f 04-mysql.yaml
kubectl apply -f 05-flask.yaml
```

## ArgoCD Setup
```bash
kubectl apply -f argocd-app.yaml --validate=false
```

## Check Status
```bash
kubectl get pods -n mytodo
minikube service flask-service -n mytodo --url
```
