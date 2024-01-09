# Lab 3

### Services

- **Basic**
```bash
kubectl get service
kubectl describe svc kubernetes
kubectl create service nodeport webapp-service --tcp=8080:8080 --node-port=30080 --dry-run=client -o yaml > service-nodeport.yaml
```