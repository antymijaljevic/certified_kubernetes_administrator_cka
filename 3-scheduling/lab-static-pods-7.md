# Lab 7

### Static pods

- **Commands**
```bash
kubectl get pods -A | wc -l
kubectl get pods -A | grep controlplane| wc -l
kubectl get pod etcd-controlplane -n kube-system -o yaml | grep kind:
```

- **Find static pod definition files path**
```bash
cat /var/lib/kubelet/config.yaml | grep staticPodPath
```

- **Create static pod**
```bash
cd /etc/kubernetes/manifests
kubectl run static-busybox --image=busybox --dry-run=client -o yaml --command -- sleep 1000 > static-busybox.yaml
```

- **SSH into node to delete static pod**
```bash
ssh node01
```
or
```bash
ssh <ip>
```