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

[Create your Amazon EKS cluster and nodes Docs - Installing eksctl](https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html)

### 3 | Create dev EKS cluster on AWS

- **Check credentials**
```bash
aws sts get-caller-identity
```

- **Create EKS cluster**
```bash
eksctl create cluster --name dev-eks-cluster --fargate
```

- **Connect your local machine with newly the created cluster (Skip this step)**
```bash
aws eks update-kubeconfig --region us-west-2
```

- **Verify resources**
```bash
kubectl get nodes -o wide
kubectl get pods -A -o wide
```

- **Delete cluster**
```bash
eksctl delete cluster --name dev-eks-cluster
```

[Encrypting Confidential Data at Rest k8s Docs](https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/)

### 4 | k8s: Encrypting Confidential Data at Rest

- **Create sample secret**
```bash
kubectl create secret generic my-secret --from-literal=key1=supersecret
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

- **Install etcd-clients**
```bash
sudo apt install etcd-client
kubectl get pods -n kube-system
```

- **Verify if secret is encrypted**
```bash
ETCDCTL_API=3 etcdctl \
   --cacert=/etc/kubernetes/pki/etcd/ca.crt   \
   --cert=/etc/kubernetes/pki/etcd/server.crt \
   --key=/etc/kubernetes/pki/etcd/server.key  \
   get /registry/secrets/default/my-secret | hexdump -C

ps -aux | grep kube-api | grep "encryption-provider-config"

cat /etc/kubernetes/manifests/kube-apiserver.yaml
```

- **Create a new encryption config file**
```yaml

```