# Docker vs Containerd

* Container tools
    * docker
    * containerD
    * rkt

* CLI Tools
    * ctr (containerD)
    * nerdctl (Docker like CLI for containerD)
    * crictl (supports all CRI compatible container runtimes)

### dockershim to support Docker integration with k8s before CRI

* Kubernetes standards
    * Container Runtime Interfaces(CRI) [Container Runtime Standard]
        * Open Container Initative (OCI)
            * imagespec
            * runtimespec

* Docker
    * CLI
    * API
    * Build
    * Volumes
    * Auth
    * Security
    * ContainerD (sparated from Docker later)

* ContainerD (individual project now)
    * ctr (cli tool)