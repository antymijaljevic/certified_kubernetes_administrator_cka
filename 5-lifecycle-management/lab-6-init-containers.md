# Lab 6

### Init containers

- **Commands**
```bash
kubectl describe pod/blue | grep -A 5 'Init Containers:'
kubectl describe pod/blue | grep -A 2 'State'
kubectl describe pod/purple | grep 'Status:'
kubectl  replace --force -f /tmp/kubectl-edit-1710992244.yaml
```

- **Log in init container**
```bash
kubectl logs orange -c init-myservice
```