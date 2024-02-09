# Lab 2

### Certificates API

- **The Certificate Signing Request**
```bash
cat akshay.key
cat akshay.csr
```

- **Create a CertificateSigningRequest**
```yaml
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: akshay
spec:
  request: <base64-encoded-csr>
  signerName: kubernetes.io/kube-apiserver-client
  usages:
  - client auth
```

```bash
cat akshay.csr | base64 -w 0
```

- **Commands**
```bash
kubectl apply -f .
kubectl get csr
kubectl certificate approve akshay
kubectl get csr agent-smith
kubectl get csr agent-smith -o yaml
kubectl certificate deny agent-smith
kubectl delete csr agent-smith
```

