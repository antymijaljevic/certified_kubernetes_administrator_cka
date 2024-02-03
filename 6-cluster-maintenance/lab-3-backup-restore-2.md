# Lab 3

### Backup and Restore Method 2

- **Commands**
```bash
k get pods -n kube-system | grep etcd
k describe pod kube-apiserver-cluster1-controlplane -n kube-system
k get pod -A
k -n kube-system describe pod etcd-cluster1-controlplane | grep data-dir
k describe pod/kube-apiserver-cluster2-controlplane -n kube-system | grep etcd-servers
```

- **ETCD default directory**
```bash
ps -ef | grep -i etcd
```

- **In/out of node**
```bash
ssh cluster2-controlplane
exit
```

- **Switch clusters**
```bash
kubectl config use-context cluster2
```

- **See all clusters**
```bash
kubectl config view
```


ETCDCTL_API=3

etcdctl --endpoints=127.0.0.1:2379 \
        --cacert=/etc/etcd/pki/ca.pem \
        --cert=/etc/etcd/pki/etcd.pem \
        --key=/etc/etcd/pki/etcd-key.pem member list

etcdctl --endpoints=https://192.28.55.9:2379 \
        --cacert=/etc/kubernetes/pki/etcd/ca.crt \
        --cert=/etc/kubernetes/pki/etcd/server.crt \
        --key=/etc/kubernetes/pki/etcd/server.key snapshot save /opt/cluster1.db


scp cluster1-controlplane:/opt/cluster1.db /opt/

ETCDCTL_API=3 etcdctl snapshot restore /root/cluster2.db --data-dir /var/lib/etcd-data-new

chown -R etcd:etcd /var/lib/etcd-data-new

vi /etc/systemd/system/etcd.service (change dir folder)

systemctl daemon-reload
systemctl restart etcd
systemctl status etcd