# Kubernetes Architecture
This document explains key components of the kubernetes cluster

## Contents
* Master node/Control-pane components
* Worker node components
* other components

![kubernetes-architecture-diagram-1](https://github.com/manojmanu276/K8s-ClusterSetUp-using-Kubeadm/assets/102495616/36795d43-0ec1-4ded-b530-ae92a3d5c74c)

## Control Pane Components

### API-Server
This is the "front desk" of Kubernetes. Whenever a request is made to create a resource in k8s, the request goes to api-server. api-server validates and authenticates this request.

### ETCD
Acts like default database of kubenetes. once api-server validates and authenticates the request, all the information is stored here in form of key-value.

### Scheduler
Scheduler finds the unscheduled pods and schedules it to the nodes.In simple terms, it can be called as "Event Planner".

### Control-Manager
The controller monitors the current state of the cluster via calls made to the API Server, and changes the current state to match the desired state described in the cluster's declarative configuration

## Worker-node Components

### Kubelet
Kubelet is the primary "node agent" that runs on each node,responsible for managing the deployment of pods to Kubernetes nodes.

### Kube-Proxy
kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.

### Container Runtime
This is the software used to run containers. Docker is commonly used, but other runtimes like containerd can also be used.

## Other Components

### Pod
Pod is the smallest manageable unit in kubernetes. Container is enclosed within the pods. Pod is a group of one or more containers.

### Namespace
namespaces are like virtual cluster inside the k8's cluster, allows different teams to use same cluster. Hence there is optimal utilisation of cluster resources.

### Ingress
Ingress is an API object that helps developers expose their applications and manage external access by providing http/s routing rules to the services within a Kubernetes cluster.

### Volumes
This is like an external hard-drive that can be attached to a Pod to store data.

### Service
Service is a method of exposing a network application that is running as one or more Pods in your cluster.

### Container Network Interface(CNI)
Container Network Interface (CNI) is a framework for dynamically configuring networking resources. In simple words, allows communication between Master node and worker nodes.(e.g. Weavenet, Flannel, Calico)
