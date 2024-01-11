# Lab 5

### Imperative VS Declarative

- **POD**
```bash
kubectl run nginx-pod --image=nginx:alpine
kubectl run redis --image=redis:alpine --labels="tier=db"
kubectl run httpd --image=httpd:alpine --port=80 --expose=true
```

- **Service (clusterIP)**
```bash
kubectl expose pod redis --port=6379 --name redis-service
```

- **Service (NodePort)**
```bash
kubectl create service clusterip redis-service --tcp=6379:6379
```

- **Deployments**
```bash
kubectl create deployment webapp --image=kodekloud/webapp-color --replicas=3
kubectl create deployment redis-deploy -n dev-ns --image=redis --replicas=2
```

- **Namespaces**
```bash
kubectl create namespace dev-ns
```

- **Apply resource (creates Last Applied Configuration)**
```bash
kubectl apply -f pod-definition.yaml 
```