### Cluster upgrade

[kubeadm-upgrade](https://v1-28.docs.kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)

- **Get cluster informations first**
```bash
kubectl get node
kubectl describe node controlplane | grep 'Taints:'
kubectl describe node node01 | grep 'Taints:'
kubectl get deployment
kubectl get pods -o wide
```

- **Get versions**
```bash
kubeadm upgrade plan
```

### Control-plane

- **Drain node and make it unschedulable**
```bash
kubectl drain controlplane --ignore-daemonsets
kubectl get pods -o wide
```

- **Check OS version and kubeadm version**
```bash
cat /etc/*release*
sudo apt update -y
kubeadm upgrade plan | grep "kubeadm version"
apt-cache madison kubeadm
```

- **Upgrade Kubeadm itself**
```bash
apt-mark unhold kubeadm && \
apt-get update && apt-get install -y kubeadm='1.27.0-00' && \
apt-mark hold kubeadm
sudo kubeadm upgrade node
kubeadm version
```

- **Upgrade k8s resources**
```bash
kubeadm upgrade plan
kubeadm upgrade apply v1.27.0 -y
```

- **Upgrade kubelet**
```bash
apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet='1.27.0-00' kubectl='1.27.0-00' && \
apt-mark hold kubelet kubectl

sudo systemctl daemon-reload && sudo systemctl restart kubelet
```

- **Drain node and make it unschedulable**
```bash
kubectl uncordon controlplane
kubectl get nodes
```

### Worker

- **Drain node01 and make it unschedulable**
```bash
kubectl drain node01 --ignore-daemonsets
kubectl get pods -o wide
```

- **SSH into node01 and repeat same process**
```bash
ssh node01
```