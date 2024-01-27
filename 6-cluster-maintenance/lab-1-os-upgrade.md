# Lab 1

### Os Upgrade

- **Commands**
```bash
kubectl get nodes
kubectl get deployments --no-headers | wc -l
kubectl get pods --output wide
kubectl describe node controlplane | grep 'Taints:'
kubectl delete pod hr-app
kubectl drain node01 --ignore-daemonsets --force
```

- **Drain node**
```bash
kubectl drain node01 --ignore-daemonsets
kubectl get node -o wide
```

- **Return node back to scheduling state**
```bash
kubectl uncordon node01
kubectl get node -o wide
```

- **Mark a node as unschedulable**
```bash
kubectl cordon node01
kubectl get node -o wide
```