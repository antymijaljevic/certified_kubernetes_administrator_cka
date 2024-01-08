# Cluster Architecture

* Cluster
    * Master Node (manage, plan, schedule, monitor nodes)
        * Container Runtime Engine (docker)
            * Kube-APIServer (orchestrating all operations within the cluster)
            * ETCD (Key-Value pair database)
            * Kube-Scheduler (identifies the righ node to place a container)
            * Controller-Manager
                * Node-Contorller
                * Repliacation-Controller
    * Worker Nodes (host containers)
        * Container Runtime Engine (docker)
            * Kubelet (An agent that runs on each node, speaks with kube-api)
            * Kube-Proxy Service (allows containers to speak with each other)