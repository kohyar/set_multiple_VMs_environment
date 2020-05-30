# How to Create a Kubernetes Cluster with kubeadm
The purpose of this part is to enable you to run a demo microservices application on a kubernetes cluster you have created.

## Prerequisites
Before you begin this tutorial, you’ll need the following:<br/>
* 3 Ubuntu servers with 4GM RAM and private networking enabled<br/>
### Step 1 - Get each server ready to run Kubernetes
Create 3 hosts and call them kube-01, kube-02 and kube-03. <br/>
* kube-01:	Master
* kube-02:	worker
* kube-03:	worker
### Step 2 - Set up each server in the cluster to run docker and Kubernetes.
On each of the three Ubuntu servers install docker and kubernetees.<br/>
To install docker on ubuntu (It's important to install like this): https://kubernetes.io/docs/setup/production-environment/container-runtimes/ <br>
To Install Kubernetes on Ubuntu: https://phoenixnap.com/kb/install-kubernetes-on-ubuntu <br/>

### Step 3: Make your cluster and add nodes
o set up a cluster and add nodes to the cluster, follow the steps after Step 6 in https://phoenixnap.com/kb/install-kubernetes-on-ubuntu <br/>
You may need to turn off swap: <code>swapoff -a</code><br/>
Sample of command to join a worker to the server:<br/>
from vm4:<br/>
<code> sudo kubeadm join 192.168.122.39:6443 --token 0vffon.2vdq471r7a7idzhp --discovery-token-ca-cert-hash sha256:677e38813c3cd96c8b60a9fcd1b4488a4bd9b9410e2839d513a6754b0133f3cb </code>

### Step 4 - Deploying The Weaveworks Microservices Sock Shop
Next we will deploy a demo microservices application to your kubernetes cluster by following the step in :<br/>
https://www.gremlin.com/community/tutorials/how-to-create-a-kubernetes-cluster-on-ubuntu-16-04-with-kubeadm-and-weave-net/

