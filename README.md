# Building a Kubernetes Cluster Setup with Minikube

## Task Overview
This project involves building and managing a Kubernetes cluster locally using Minikube. The task includes deploying a sample NGINX application, exposing it using a Kubernetes service, scaling the deployment, and viewing logs for troubleshooting.

## Objectives
- Deploy and manage applications in Kubernetes.
- Learn basic Kubernetes concepts like Pods, Deployments, Services, and scaling.
- Gain hands-on experience with Minikube and kubectl.

## Tools Used
- **Minikube**: A tool to run Kubernetes clusters locally.
- **kubectl**: A command-line tool to interact with Kubernetes clusters.
- **Docker**: Used as the driver for Minikube.
- **NGINX**: Deployed as a sample app.

## Prerequisites
- **Minikube** installed and running.
- **kubectl** installed and configured to interact with the Minikube cluster.
- Docker installed and set up.

## Steps to Complete

### 1. Install Minikube & kubectl
Follow these steps to install Minikube and kubectl:

1. Install Minikube using the official instructions for your system.
2. Install kubectl to interact with the Kubernetes cluster.

### 2. Start Minikube
Start your Minikube cluster with Docker as the driver:

```bash
minikube start --driver=docker


Verify the status:
minikube status

3. Create Deployment YAML
Create a file deployment.yaml for the NGINX app deployment.

apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80

Apply the deployment:
Create a service.yaml to expose the deployment:

apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80

Apply the service:
kubectl apply -f service.yaml

5. Scale the Deployment
Scale the deployment to 4 replicas:
kubectl scale deployment my-nginx --replicas=4

Verify scaling:
kubectl get pods

6. View Logs
To view logs for any pod:

kubectl logs myngix-***********

To view logs for all pods:
kubectl logs -l app=nginx --all-containers=true

7. Describe the Deployment
Get detailed information about the deployment:
kubectl describe deployment my-nginx


Outcome
By the end of this task, the following actions were completed successfully:

Deployed the NGINX app to the Kubernetes cluster.

Exposed the app via a service.

Scaled the app deployment to 4 replicas.

Viewed logs and descriptions of the deployment.



Future Improvements
Explore Persistent Storage in Kubernetes.

Use Helm to manage deployments and services more efficiently.

Scale the app with Horizontal Pod Autoscaling.
