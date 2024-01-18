# Lab 1

### PODS

- **Commands**
```bash
kubectl get pods
kubectl run nginx --image=nginx
kubectl describe <pod-name>
kubectl delete pod <pod-name>
```

- **More information about pods (including node)**
```bash
kubectl get pod -o wide
```

- **Pod dry run with yaml export**
```bash
kubectl run <pod-name> --image=<image-name> --dry-run=client -o yaml > <pod-name>.yaml
```

- **Create pod from yaml**
```bash
kubectl create -f <pod-name>.yaml
```

- **Edit pod definition**
```bash
vi <pod-name>.yaml
kubectl apply -f <pod-name>.yaml
```
or
```bash
kubectl edit pod <pod-name>
```


