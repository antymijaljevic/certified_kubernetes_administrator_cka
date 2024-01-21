# Lab 3

### Envronment Variables

- **Envronment Variables**
```bash
kubectl describe pod ubuntu-sleeper | grep -A 2 'Command:'
kubectl edit pod webapp-color
kubectl replace --force -f /tmp/kubectl-edit-1395526044.yaml
```

- **ConfigMaps**
```bash
kubectl get configmaps
kubectl get cm
kubectl describe cm db-config
kubectl create configmap webapp-config-map --from-literal=APP_COLOR=darkblue --from-literal=APP_OTHER=disregard
```