# Lab 2

### Application logs

- **Run metrics server on minikube**
```bash
kubectl get pods
kubectl logs webapp-1 -f
kubectl logs webapp-1 image1
kubectl logs webapp-1 image2
```