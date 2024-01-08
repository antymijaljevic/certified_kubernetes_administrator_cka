# Lab 1

### PODS

- **Basic**
```
kubectl get pods
kubectl run nginx --image=nginx
kubectl describe <pod-name>
kubectl delete pod <pod-name>
```

- **More information about pods (including node)**
```
kubectl get pod -o wide
```

- **Pod dry run with yaml export**
```
kubectl run <pod-name> --image=<image-name> --dry-run=client -o yaml > <pod-name>.yaml
```

- **Create pod from yaml**
```
kubectl create -f <pod-name>.yaml
```

- **Edit pod definition**
```
vi <pod-name>.yaml
kubectl apply -f <pod-name>.yaml
```
or
```
kubectl edit pod <pod-name>
```


