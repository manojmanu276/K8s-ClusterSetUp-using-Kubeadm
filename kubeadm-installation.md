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
```
sudo kubeadm init
![k 1](https://github.com/manojmanu276/K8s-ClusterSetUp-using-Kubeadm/assets/102495616/5e4a3414-41b3-4cfb-8ed1-84b40b621192)
```
