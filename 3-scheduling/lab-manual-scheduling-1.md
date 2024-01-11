# Lab 1

### Scheduler

- **K8s core services**
```bash
kubectl get pods -n kube-system
```

- **Force pod recreation**
```bash
kubectl replace --force -f nginx.yaml
```

- **Monitor creation**
```bash
kubectl get pods --watch
kubectl get pods -o wide
```