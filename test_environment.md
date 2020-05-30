# How to Create a Kubernetes Cluster with kubeadm
The purpose of this part is to enable you to run a demo microservices application on a kubernetes cluster you have created.

## Prerequisites
Before you begin this tutorial, you’ll need the following:<br/>
* 3 Ubuntu servers with 4GM RAM and private networking enabled<br/>
### Step 1 - Get each server ready to run Kubernetes
Create 3 hosts and call them kube-01, kube-02 and kube-03. <br/>
* kube-01:	Master
* kube-02:	Node
* kube-03:	Node
### Step 2 - Set up each server in the cluster to run Kubernetes.
On each of the three Ubuntu servers install docker and kubernetees.<br/>
To install docker on ubuntu: https://kubernetes.io/docs/setup/production-environment/container-runtimes/ <br>
You may need to turn off swap: <code>swapoff -a</code><br/>
To Install Kubernetes on Ubuntu: https://phoenixnap.com/kb/install-kubernetes-on-ubuntu <br/>
### Step 3 - Setup the Kubernetes Master


sudo kubeadm join 192.168.122.184:6443 --token 6vnyre.u3dxx9ryrlbdyhy9     --discovery-token-ca-cert-hash sha256:a46ad1069d5e94face27f715270d20be891774654c0aebabf2c8571afa486450


