# Lab 3

### Deployments

- **Basic**
```
kubectl get deployments
kubectl create -f nginx-deployment.yaml
kubectl describe deployment <deployment-name>
kubectl create deployment --help
```

- **Creating resources without YAML**
```
kubectl run nginx --image=<image>
kubectl create deployment <dep-name> --image=<image> --replicas=<n>
```

- **Generate Deployment YAML file (-o yaml). Don't create it (--dry-run)**
```
kubectl create deployment --image=nginx nginx --dry-run=client -o yaml
kubectl run nginx --image=nginx --dry-run=client -o yaml
kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml
kubectl create deployment --image=nginx nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml
```
