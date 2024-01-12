# Lab 2

### Labels and Selectors

- **Basic**
```bash
kubectl get pods --selector app=app-1
kubectl get all --selector env=prod
kubectl get pod --selector env=prod,bu=finance,tier=frontend
```