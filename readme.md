# Building a simple app using node.js and deploying on [Kubernetes](https://kubernetes.io/) using [minikube](https://kubernetes.io/docs/getting-started-guides/minikube/)


## Prerequisites 

* Docker as per the OS, [Docker CE](https://docs.docker.com/install/) 
* Install [xhyve](https://github.com/zchee/docker-machine-driver-xhyve#install) driver 
* [NodeJS](https://nodejs.org/en/download/) 
 

## 1) Building a minikube cluster 
1. Install [minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/) as per the OS

2. Install [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) as per the OS

For OSX:
```
brew install kubectl
```
3. Check if you have an access to [Google Cloud](https://cloud.google.com/container-registry/)
```
curl --proxy "" https://cloud.google.com/container-registry/
```
4. Start the minikube cluster (without proxy)
```
minikube start --vm-driver=xhyve
```
5. Access Kubernetes dashboard
```
minikube dashboard
```
## 2) Running a Node.js app
Run the application using following command: 
```
node server.js
```

## 3) Dockerize the Node.js app
1. After creating a Dockerfile, make sure to use Minikube Docker daemon by executing following command:
```
eval $(minikube docker-env)
```
2. Check a Dockerfile in this repo and use following command to build a Docker image:
```
docker build -t test-node:v1 .
```

## 4) Deploy the app on Kubernetes 

1. Create depolyment using following command:
```
kubectl run test-node --image=test-node:v1 --port=8080
```
2. view deployments:
```
kubectl get deployments
```
3. View Kubenetes [POD](https://kubernetes.io/docs/concepts/workloads/pods/pod/):
```
kubectl get pods
```
Also, make sure to check Kubernetes dashboard to see more details of the deployed app under Workloads/Depolyments. 




