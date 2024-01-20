# Lab 2

### Commands and Arguments

- **Commands**
```bash
kubectl describe pod ubuntu-sleeper | grep -A 2 'Command:'
kubectl apply -f ubuntu-sleeper-2.yaml
```

- **Run pod with command (ENTRYPOINT)**
```bash
kubectl run ubuntu --image=ubuntu:latest --command sleep 5000
```

- **Run pod with arguments (CMD)**
```bash
kubectl run webapp-green --image=kodekloud/webapp-color -- --color green
```