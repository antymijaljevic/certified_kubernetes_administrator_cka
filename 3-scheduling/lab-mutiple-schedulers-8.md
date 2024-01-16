# Lab 8

### Multiple Schedulers

- **Basic**
```bash
kubectl describe pod kube-scheduler-controlplane -n kube-system | grep Image:
kubectl get all -A
kubectl get sa my-scheduler -n kube-system
kubectl create configmap my-scheduler-config --from-file=/root/my-scheduler-config.yaml -n kube-system
kubectl get configmap my-scheduler-config -n kube-system
```