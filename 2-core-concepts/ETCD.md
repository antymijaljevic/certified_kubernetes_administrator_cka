# ETCD is a distributed reliable key-value store

* ETCD
    * Port 2379
    * ETCD Client


### ETCD Commands

- **ETCDCTL version 2**
```
etcdctl --version
etcdctl backup
etcdctl cluster-health
etcdctl mk
etcdctl mkdir
etcdctl set
```

- **ETCDCTL version 3**
```
etcdctl version
etcdctl snapshot save 
etcdctl endpoint health
etcdctl get
etcdctl put
```

- **Set API version**
```
export ETCDCTL_API=3
```

- **Certificate files so that ETCDCTL can authenticate**
```
--cacert /etc/kubernetes/pki/etcd/ca.crt     
--cert /etc/kubernetes/pki/etcd/server.crt     
--key /etc/kubernetes/pki/etcd/server.key
```

- **Full command example**
```
kubectl exec etcd-master -n kube-system -- sh -c "ETCDCTL_API=3 etcdctl get / --prefix --keys-only --limit=10 --cacert /etc/kubernetes/pki/etcd/ca.crt --cert /etc/kubernetes/pki/etcd/server.crt  --key /etc/kubernetes/pki/etcd/server.key"
```