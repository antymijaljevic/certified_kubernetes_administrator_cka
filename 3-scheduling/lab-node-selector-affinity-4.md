# Lab 4

### Node Selectors & Affinity

- **Basic**
```bash
kubectl describe node node01
kubectl label node node01 color=blue
kubectl create deployment blue --image=nginx --replicas=3
kubectl get all -o wide
kubectl describe node node01 | grep Taints:
kubectl get nodes --show-labels
kubectl create deployment red --image=nginx --replicas=2 --dry-run=client -o yaml >red.yaml
```