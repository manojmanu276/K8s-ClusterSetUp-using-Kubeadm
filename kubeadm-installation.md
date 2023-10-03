# Kubeadm Installation Guide
This guide contains all the necessary steps to set up kubernetes cluster using kubeadm

## Pre-requisites
* Ubuntu Os (Xenial(16.04) or later)
* EC2-Instance (t2.medium or higer)
* sudo privileges

## Commands to be Executed in both Master & Worker node
Run the following commands in both worker node and master node to prepare them for kubeadm
```
sudo apt update
sudo apt-get install -y apt-transport-https ca-certificates curl
sudo apt install docker.io -y

sudo systemctl enable --now docker # enable and start in single command.

# Adding GPG keys.
curl -fsSL "https://packages.cloud.google.com/apt/doc/apt-key.gpg" | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/kubernetes-archive-keyring.gpg

# Add the repository to the sourcelist.
echo 'deb https://packages.cloud.google.com/apt kubernetes-xenial main' | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt update 
sudo apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y
```
## Commands to be Execute in the master node
1. Initialize the Kubernetes on master node
```
sudo kubeadm init
```
![k 1](https://github.com/manojmanu276/K8s-ClusterSetUp-using-Kubeadm/assets/102495616/5e4a3414-41b3-4cfb-8ed1-84b40b621192)

After succesfully running, your Kubernetes control plane will be initialized successfully.

![k 2](https://github.com/manojmanu276/K8s-ClusterSetUp-using-Kubeadm/assets/102495616/dd9d2b80-32ea-4b20-a72a-e11ae1c6f430)

2. Set up local kubeconfig (both for root user and normal user):
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
![k 3](https://github.com/manojmanu276/K8s-ClusterSetUp-using-Kubeadm/assets/102495616/010b2da4-c85a-4c4f-8a51-766d1777af91)

3. Apply Weave Network (enables communication between master and worker node)
```
kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
```
![k 4](https://github.com/manojmanu276/K8s-ClusterSetUp-using-Kubeadm/assets/102495616/30d0419b-0bc2-4387-a103-84968094a9e6)

4. Generate Token in Master node for worker nodes to join the cluster
```
sudo kubeadm token create --print-join-command
```
![k 5](https://github.com/manojmanu276/K8s-ClusterSetUp-using-Kubeadm/assets/102495616/85da39e3-90f9-4985-857a-bd9ad468cef5)

5. Expose port 6443 in the Security group Inbound rules of Control-pane for the Worker to connect to Master Node

![k 6](https://github.com/manojmanu276/K8s-ClusterSetUp-using-Kubeadm/assets/102495616/30630dc5-c1c3-44a0-b83f-6fe242697b2f)

## Commands to be Executed in the Worker Nodes

1. Run the following commands in the worker node.

![k 7](https://github.com/manojmanu276/K8s-ClusterSetUp-using-Kubeadm/assets/102495616/cae58e0a-eca9-483f-a6f9-c280d96fbf5a)

2. Paste the join command you got from the master node and add --v=5 at the end. Make sure you execute this command as the root user

![k 8](https://github.com/manojmanu276/K8s-ClusterSetUp-using-Kubeadm/assets/102495616/4bd27dc8-3162-43b9-a823-ae15d29b2628)

   After executing the above command, you get the below message:

![k 9](https://github.com/manojmanu276/K8s-ClusterSetUp-using-Kubeadm/assets/102495616/5a32c54b-42b8-47e6-9d6c-fd072430b0a8)

## Verify Cluster Connection
```
kubectl get nodes
```
![k 10](https://github.com/manojmanu276/K8s-ClusterSetUp-using-Kubeadm/assets/102495616/3033d461-9daf-448e-a261-a294d559c03f)






