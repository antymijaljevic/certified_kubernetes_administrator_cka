# Lab 5

### Namespaces

- **Basic**
```bash
kubectl create namespace dev
kubectl get namespaces
kubectl create -f pod-definition.yaml --namespace=dev
kubectl get pods --namespace=kube-system
```

- **Prenamently switch namespace**
```bash
kubectl config set-context $(kubectl config current-context) --namespace=dev
```

- **List all resources in all namespaces**
```bash
kubectl get all --all-namespaces
```