# Lab 1

### Monitoring

- **Run metrics server on minikube**
```bash
minikube addons enable metrics-server
kubectl get all --namespace kube-system
```

- **Install metrics server**
```bash
git clone https://github.com/kodekloudhub/kubernetes-metrics-server.git
kubectl create -f .
```

- **Metrics**
```bash
kubectl get pods
kubectl top node
kubectl top pod
```
