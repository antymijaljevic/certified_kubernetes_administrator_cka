# TLS in Kubernetes

### Symmetric encryption

* Symmetric encryption
    * Using the same key do encrypt and decrypt

- **Generate private and public key pair**
```bash
openssl genrsa -out <name>.key 1024
openssl genrsa -in <name>.key -pubout > <name>.pem
```