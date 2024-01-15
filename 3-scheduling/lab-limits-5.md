# Lab 5

### Resource requirements and limits

- **Can't change RAM while container is running**
```bash
kubectl edit pod elephant
```

- **Recreate pod with a new config**
```bash
kubectl replace --force -f /tmp/kubectl-edit-2818244031.yaml
```
