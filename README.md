# K8s Tutorials Helm Charts
This repository contains 4 Helm charts that following the tutorials.

## Prerequisites
1. [Docker](https://docs.docker.com/get-docker/)
2. [Minikube](https://minikube.sigs.k8s.io/docs/start/)
3. [Helm 3](https://helm.sh/docs/intro/install/)

## Getting Started
1. Install prerequisites tool above.
2. Start the minikube cluster.
   ```bash
   $ minikube start
   ```

## Exercise Helm Charts
### 1. Example: Deploying PHP Guestbook application with Redis ([https://kubernetes.io/docs/tutorials/stateless-application/guestbook/](https://kubernetes.io/docs/tutorials/stateless-application/guestbook/))

To perform helm deployment, do the following  
```bash
$ helm upgrade --install guestbook ./php-guestbook
```

### 2. Example: Deploying WordPress and MySQL with Persistent Volumes ([https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/](https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/))

To perform helm deployment, do the following  
1. Generate deployment.yaml by templates.
```bash
$ helm template ./wordpress-mysql > ./wordpress-mysql/outputs/deployment.yaml
```
2. Apply kustomization.yaml secret.
```bash
$ kubectl kustomize ./wordpress-mysql/outputs > ./wordpress-mysql/templates/deployment.yaml
```
3. Perform the deployment.
```bash
$ helm upgrade --install wordpress ./wordpress-mysql --set template.enabled=false
```