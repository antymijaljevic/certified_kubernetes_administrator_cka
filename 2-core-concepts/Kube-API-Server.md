# Kube-API Server

### Kube-API Commands

* Flow
    1. Authenticate user
    2. Validate Request
    3. Retrieve data
    4. Update ETCD
    5. Scheduler
    6. Kubelet

- **Show nodes**
```
kubectl get nodes
```

### Kube Controller Manager (Watch status & Remediate situation)

* Contollers
    * Node Controller
    * Replication Controller
    * Endpoints Controller
    * Service Account & Token Controllers
    * Persistent Volume (PV) Controller
    * Persistent Volume Claim (PVC) Controller
    * Namespace Controller
    * Service Controller
    * DaemonSet Controller
    * Job Controller
    * StatefulSet Controller

- **List K8s services (kubeadm)**
```
kubectl get pods -n kube-system
```