# K8s Tutorials Helm Charts
This repository contains 4 Helm charts that following the tutorials.

# Prerequisites
1. [Docker](https://docs.docker.com/get-docker/)
2. [Minikube](https://minikube.sigs.k8s.io/docs/start/)
3. [Helm 3](https://helm.sh/docs/intro/install/)

# Getting Started
1. Install prerequisites tool above.
2. Start the minikube cluster.
   ```bash
   $ minikube start
   ```

## 1. Example: Deploying PHP Guestbook application with Redis ([https://kubernetes.io/docs/tutorials/stateless-application/guestbook/](https://kubernetes.io/docs/tutorials/stateless-application/guestbook/))

To perform helm deployment, do the following  
```bash
$ helm upgrade --install guestbook ./php-guestbook
```