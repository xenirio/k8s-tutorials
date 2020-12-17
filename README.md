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

To perform helm deployment:
```bash
$ helm upgrade --install guestbook ./php-guestbook
```
To get the IP address for the frontend Service:
```bash
$ minikube service frontend --url
```
To uninstall resources:
```bash
$ helm uninstall guestbook
```

### 2. Example: Deploying WordPress and MySQL with Persistent Volumes ([https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/](https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/))

To perform helm deployment:
1. Generate deployment.yaml by templates
```bash
$ helm template ./wordpress-mysql > ./wordpress-mysql/outputs/deployment.yaml
```
2. Apply kustomization.yaml secret
```bash
$ kubectl kustomize ./wordpress-mysql/outputs > ./wordpress-mysql/templates/deployment.yaml
```
3. Perform the deployment
```bash
$ helm upgrade --install wordpress ./wordpress-mysql --set template.enabled=false
```
To get the IP address for the wordpress Service:
```bash
$ minikube service wordpress --url
```
To uninstall resources:
```bash
$ helm uninstall wordpress
```

### 3. Example: Deploying Cassandra with a StatefulSet ([https://kubernetes.io/docs/tutorials/stateful-application/cassandra/](https://kubernetes.io/docs/tutorials/stateful-application/cassandra/))

To perform helm deployment:
1. Remove and recreate Minikube to avoid insufficient resource, start Minikube with the following settings
```bash
$ minikube delete
$ minikube start --memory 5120 --cpus=4
```
2. Perform the deployment
```bash
$ helm upgrade --install cassandra ./cassandra-statefulset
```
To get Cassandra StatefulSet:
```bash
$ kubectl get statefulset cassandra
```
To uninstall resources:
```bash
$ helm uninstall cassandra
```

### 4. Running ZooKeeper, A Distributed System Coordinator ([https://kubernetes.io/docs/tutorials/stateful-application/zookeeper/](https://kubernetes.io/docs/tutorials/stateful-application/zookeeper/))

You will require a cluster with at least four nodes, and each node requires at least 2 CPUs and 4 GiB of memory.
So, I perform the deployment with the GKE cluster.

To perform helm deployment:
1. Connect to the GKE cluster
```bash
$ gcloud container clusters get-credentials [cluster name] --zone [zone] --project [project id]
```
2. Perform the deployment
```bash
$ helm upgrade --install zookeeper ./zookeeper-coordinator
```
3. Check the StatefulSet's Pods, Use `CTRL-C` to terminate to kubectl when all Pods is running.
```bash
$ kubectl get pods -w -l app=zk
```
To uninstall resources:
```bash
$ helm uninstall zookeeper
```