# Lab 1

### View certs

- **Certificate file used for the kube-api server**
```bash
cat /etc/kubernetes/pki/apiserver.crt
```

- **Certificate file used to authenticate kube-apiserver as a client to ETCD Server**
```bash
cat /etc/kubernetes/manifests/kube-apiserver.yaml | grep etcd-certfile
```

- **The key used to authenticate kubeapi-server to the kubelet server**
```bash
cat /etc/kubernetes/manifests/kube-apiserver.yaml | grep kubelet-client-key
```

- **the ETCD Server Certificate used to host ETCD server**
```bash
cat /etc/kubernetes/manifests/etcd.yaml | grep cert-file
```

- **the ETCD Server CA Root Certificate used to serve ETCD Server**
```bash
cat /etc/kubernetes/manifests/etcd.yaml | grep trusted-ca-file
```

- **the ETCD Server CA Root Certificate used to serve ETCD Server**
```bash
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text | grep Subject
```

- **the name of the CA who issued the Kube API Server Certificate**
```bash
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text | grep Issuer
```

- **DNS names on Kube API Server**
```bash
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text | grep DNS:
```

- **The Common Name (CN) configured on the ETCD Server certificate**
```bash
openssl x509 -in /etc/kubernetes/pki/etcd/server.crt -text | grep Subject
```

- **How long, from the issued date, is the Kube API Server cert**
```bash
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text | grep Not
```

- **How long, from the issued date, is the Root CA Certificate valid for**
```bash
openssl x509 -in /etc/kubernetes/pki/ca.crt -text | grep Not
```

12/13
