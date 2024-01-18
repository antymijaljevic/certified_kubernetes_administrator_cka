# Lab 3

### Deployments

- **Commands**
```bash
kubectl get deployments
kubectl create -f <deployment-name>.yaml
kubectl describe deployment <deployment-name>
kubectl create deployment --help
kubectl delete deployment <deployment-name>
```

- **Rolling deployments and Rollback**
### Create
```bash
kubectl create -f rollout.yaml
kubectl apply -f rollout.yaml
```

### Rolling deployment 100/200
```bash
kubectl replace -f rollout-2.yaml
kubectl set image deployment myapp-deployment nginx-container=nginx:stable
kubectl edit deployment myapp-deployment --record
```

### Status, Record and History (record has been deprecated)
```bash
kubectl create -f deployment-rolling.yaml --record 
kubectl rollout status deployment/myapp-deployment
kubectl rollout history deployment myapp-deployment
```

### Rollback
```bash
kubectl rollout undo deployment myapp-deployment
```

- **Creating resources without YAML**
```bash
kubectl run nginx --image=<image>
kubectl create deployment <dep-name> --image=<image> --replicas=<n>
```

- **Generate Deployment YAML file (-o yaml). Don't create it (--dry-run)**
```bash
kubectl create deployment --image=nginx nginx --dry-run=client -o yaml
kubectl run nginx --image=nginx --dry-run=client -o yaml
kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml
kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml
```
