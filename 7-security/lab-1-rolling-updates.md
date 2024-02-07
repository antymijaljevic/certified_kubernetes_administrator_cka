# Lab 1

### Rolling updates and rollbacks

- **Commands**
```bash
kubectl edit deploy frontend
kubectl set image deployment frontend simple-web-app=kodekloud/webapp-color:v2
kubectl get pods --watch
```