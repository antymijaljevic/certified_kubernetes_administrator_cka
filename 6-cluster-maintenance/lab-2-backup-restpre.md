# Lab 2

### Backup and Restore

- **Commands**
```bash
kubectl get deployments
kubectl get pods -n kube-system
kubectl describe pod etcd-controlplane -n kube-system | grep image
```

- **ETCD Informations for Backup**
```bash
kubectl describe pod etcd-controlplane -n kube-system | grep -e listen-client-urls server.crt -e ca.crt -e server.key
```

- **Paths to know**
```bash
cat /etc/kubernetes/manifests/etcd.yaml
ls /var/lib/etcd/member/
ls /etc/kubernetes/pki/
```

- **Saving Snapshot**
```bash
export ETCDCTL_API=3

etcdctl snap save --endpoints=127.0.0.1:2379 \
                  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
                  --cert=/etc/kubernetes/pki/etcd/server.crt \
                  --key=/etc/kubernetes/pki/etcd/server.key \
                  /opt/snapshot-pre-boot.db

cat /opt/snapshot-pre-boot.db
```

- **Extracting Snapshot**
```bash
etcdctl snapshot restore --data-dir /var/lib/etcd-from-backup /opt/snapshot-pre-boot.db

ls /var/lib/etcd/member/
```

- **Restoring Snapshot**
```bash
### hostPath to > /var/lib/etcd-from-backup
vi /etc/kubernetes/manifests/etcd.yaml

kubectl delete pod/etcd-controlplane -n kube-system

kubectl get all -A --watch
```