# Lab 6

### Daemon Sets

- **Commands**
```bash
kubectl get daemonsets --all-namespaces
kubectl get daemonsets --all-namespaces -o wide
kubectl describe pod kube-flannel-ds --namespace kube-flannel
kubectl create deployment elasticsearch -n kube-system --image=registry.k8s.io/fluentd-elasticsearch:1.20 --dry-run=client -o yaml > new.yaml
kubectl get ds
```