[KubeConfig](https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/)

### CubeConfig

- **Configure KubeConfig file**
```bash
~/.kube/config
```

- **View configs**
```bash
kubectl config view
```

- **View configs**
```bash
kubectl config view
```

- **Use specific config**
```bash
kubectl config --kubeconfig=/root/my-kube-config use-context research
```

- **Current context**
```bash
kubectl config --kubeconfig=/root/my-kube-config current-context
test-user@development
```
