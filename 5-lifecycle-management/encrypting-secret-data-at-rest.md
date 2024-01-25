# Encryption Secret Data at Rest 

## Create dev EKS cluster on AWS

[Amazon EKS Docs - AWS CLI install](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

### 0 | Installing AWS CLI

- **Download and install**
```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```
- **Add to PATH permanently (restart terminal)**
```bash
sudo -s
echo -e '# aws cli\nexport PATH=$PATH:/usr/bin/aws' >> /etc/profile
aws --version
```
- **Set credentials**
```bash
aws configure
```

[Amazon EKS Docs - Installing kubectl](https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html)

### 1 | Installing kubectl

- **Download**
```bash
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.28.5/2024-01-04/bin/linux/amd64/kubectl
```
- **Verify the downloaded binary**
```bash
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.28.5/2024-01-04/bin/linux/amd64/kubectl.sha256
```
- **Check the SHA-256 checksum**
```bash
sha256sum -c kubectl.sha256 && openssl sha1 -sha256 kubectl
```
- **Permissions and binary**
```bash
chmod +x ./kubectl
mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl
```
- **Add to PATH permanently (restart terminal)**
```bash
sudo -s
echo -e '# kubectl\nexport PATH=$HOME/bin:$PATH' >> /etc/profile
```
- **Verify version**
```bash
kubectl version --client
```

[Amazon EKS Docs - Installing eksctl](https://eksctl.io/installation/#)

### 2 | Installing eksctl

- **Setup env variables**
```bash
ARCH=amd64 && PLATFORM=$(uname -s)_$ARCH
```
- **Download**
```bash
curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"
```
- **Check the SHA-256 checksum**
```bash
curl -sL "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_checksums.txt" | grep $PLATFORM | sha256sum --check
```
- **Extract and install**
```bash
tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz && sudo mv /tmp/eksctl /usr/local/bin
```

- **Add to PATH permanently (restart terminal)**
```bash
sudo -s
echo -e '# eksctl\nexport PATH=$HOME/usr/local/bin:$PATH' >> /etc/profile
```
- **Verify version**
```bash
eksctl version
```

### 3 | Install Minikube

[Minikube](https://minikube.sigs.k8s.io/docs/start/)
- **Install minikube**
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
- **Setup MiniKube**
```bash
minikube start --container-runtime=docker --driver=docker
```
- **Verify that prerequisites are installed**
```bash
docker ps && kubectl version && minikube version
```

[Encrypting Confidential Data at Rest k8s Docs](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)

### 4 | k8s: Encrypting Confidential Data at Rest

- **Create sample secret**
```bash
c
```

- **Describe secret (encoded in base64)**
```bash
kubectl describe secret my-secret
```

- **Base64**
```bash
kubectl get secret my-secret -o yaml
echo "c3VwZXJzZWNyZXQ=" | base64 --decode
echo "supersecret" | base64
```

- **Verify etcd-minikube pod**
```bash
kubectl get pods -n kube-system | grep etcd
```

- **Install etcd-client and Hexdump (minikube ssh)**
```bash
sudo -s
apt update
apt install etcd-client
apt-get install bsdmainutils
etcdctl --version && hexdump --version
```

- **Verify if secret is encrypted (minikube ssh)**
```bash
ETCDCTL_API=3 etcdctl \
   --cacert=/var/lib/minikube/certs/etcd/ca.crt   \
   --cert=/var/lib/minikube/certs/etcd/server.crt \
   --key=/var/lib/minikube/certs/etcd/server.key  \
   get /registry/secrets/default/my-secret | hexdump -C
```

- **Verify if there are encryption on flags (returns nothing is false)**
```bash
ps -aux | grep kube-api | grep "--encryption-provider-config"
cat /etc/kubernetes/manifests/kube-apiserver.yaml | grep encryption
```

- **Start by generating a new encryption key, and then encode it using base64**
```bash
head -c 32 /dev/urandom | base64
```

- **Create a new encryption config file**
```bash
cat <<EOF > /etc/kubernetes/enc/enc.yaml
apiVersion: apiserver.config.k8s.io/v1
kind: EncryptionConfiguration
resources:
  - resources:
      - secrets
    providers:
      - aescbc:
          keys:
            - name: key1
              # See the following text for more details about the secret value
              secret: GbMAlnyvINEBTOo7Ac23S7SFRg6djIm1PK4Otk9K7VU== # put here generated key
      - identity: {} # this fallback allows reading unencrypted secrets;
                     # for example, during initial migration
EOF
```

nano /etc/kubernetes/manifests/kube-apiserver.yaml

    - --encryption-provider-config=/etc/kubernetes/enc/enc.yaml

        - mountPath: /etc/kubernetes/enc
      name: enc
      readOnly: true

  - name: enc
    hostPath:
      path: /etc/kubernetes/enc
      type: DirectoryOrCreate



kubectl create secret generic my-secret-2 --from-literal=key1=topsecret

ETCDCTL_API=3 etcdctl \
   --cacert=/var/lib/minikube/certs/etcd/ca.crt   \
   --cert=/var/lib/minikube/certs/etcd/server.crt \
   --key=/var/lib/minikube/certs/etcd/server.key  \
   get /registry/secrets/default/my-secret-2 | hexdump -C