# https://kubernetes.io/docs/tasks/tools/

- **install Docker engine (install Docker Desktop for Win11)**

- **Install kubectl**
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256) kubectl" | sha256sum --check
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
```

- **Install minikube**
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube version
```

- **Setup MiniKube**
```bash
minikube start --container-runtime=docker --driver=docker
docker ps && kubectl version && minikube version
```

- **Get inside MiniKube**
```bash
minikube ssh
docker ps
exit
```

- **Remove MiniKube**
```bash
minikube stop
minikube delete
```

- **Minikube k8s cluster information**
```bash
kubectl get nodes
kubectl get nodes -o wide
kubectl describe node minikube
```


### Sample deployment with CLI

- **Sample deployment**
```bash
kubectl create deployment nginx --image=nginx:stable
kubectl get all
kubectl expose deployment nginx --type=NodePort --port=80
minikube service nginx --url
```

- **Minikube IP address**
```bash
minikube ip
```

- **Expose service on Minikube**
```bash
minikube service <service-name>
```

### Sample deployment with yaml files
```bash
cd sample-deployment && kubectl apply -f .
```

- **Remove sample deployment**
```bash
kubectl delete --all deployments,services,pods
```