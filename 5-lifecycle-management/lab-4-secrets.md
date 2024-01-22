# Lab 4

### Secrets

- **Create secret from yaml**
```bash
kubectl get secrets
kubectl describe secret  dashboard-token
kubectl create -f secret.yaml
```

- **Create secret imperative way**
```bash
kubectl create secret generic db-secret-2 --from-literal DB_Host=sql01 --from-literal DB_User=root --from-literal DB_Password=password123
```