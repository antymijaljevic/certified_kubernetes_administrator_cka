# Lab 3

### Taints and Tolerations

- **Commands**
```bash
kubectl get nodes -o wide

kubectl describe node controlplane | grep Taint
kubectl run mosquito --image=nginx
kubectl describe pod  mosquito
kubectl describe pod/mosquito | grep Node:
```

- **Taint node**
```bash
kubectl taint node node01 spray=mortein:NoSchedule
kubectl describe node node01 | grep Taints
```

- **Add toleration on pod**
```bash
kubectl run bee --image=nginx --dry-run=client -o yaml > bee.yaml
```
```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: bee
  name: bee
spec:
  containers:
  - image: nginx
    name: bee
  tolerations:
    - key: spray
      value: mortein
      effect: NoSchedule
      operator: Equal
```

- **Remove taint from node**
```bash
kubectl edit node controlplane
```
or
```bash
kubectl taint node controlplane <taint value>-
```