# Lab 5

### Multi Container Pods

- **Commands**
```bash
kubectl describe pod/red
kubectl get pod --namespace elastic-stack
kubectl logs kibana --namespace elastic-stack
kubectl -n elastic-stack logs kibana --follow
kubectl -n elastic-stack exec -it pod/app -- sh
kubectl -n elastic-stack edit pod/app
kubectl replace --force -f /tmp/kubectl-edit-144835156.yaml
```
