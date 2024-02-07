# TLS Certs

### Symmetric encryption

* Symmetric encryption
    * Using the same key do encrypt and decrypt

- **Generate private and public key pair**
```bash
openssl genrsa -out <name>.key 1024
openssl genrsa -in <name>.key -pubout > <name>.pem
```

1. The symmetric key (SE) that we use to encrypt data is sent together with the encrypted data (hacker getting the key).

2. On the first access to the website, the user gets the public key (hacker gets the public key).

3. The user's browser then encrypts the symmetric key using the public key given by the server. The symmetric key is now secured (hacker also gets this but doesn't have the private key).

4. The server uses the private key to decrypt the symmetric key and now has it for further communication (hacker doesn't have the private key to decrypt the symmetric key).

5. Now they both have symmetric key and faster communicaton.

### Asymmetric encryption

* Asymmetric encryption
    * Using key pair (private and public [lock])

- **Generate private and public key pair**
```bash
ssh-keygen
cat ~/.ssh/authorized_keys
```