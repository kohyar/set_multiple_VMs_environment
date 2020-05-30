# Setting up multiple VMs and the required tools for anomaly detection in microservice environment project
Some useful references to know more about microservices:
 * https://www.nginx.com/blog/deploying-microservices/

To set up multiple VMs on GUI-less virtualbox read VBox/VBoxSetup.md <br/>
To set up multiple VMs using kvm read KVM/KVM_Setup.md <br/>

## Install the required tools on VMs
After setting up an ubuntu virtual machine we run the <code>VMRequirement</code> script to install required following packages:<br/>
* Install git on guest(done)
* Install Python2 &3 on guest(done)
* Install Pumba on guest (done)
* Install Stress and Stress-ng on guest (done)
* Install cAdvisor on guest (done)
* Install Docker and Docker compass on guest (done)(Installation is not in script)
* Install Jaeger on guest (done)
* Install our application to Query performance metrics in each node

Running cAdvisor in a Docker Container(we cloned the cAdvisor from it's repository in script):<br/>
<code>VERSION=v0.35.0 # use the latest release version from https://github.com/google/cadvisor/releases
sudo docker run \
  --volume=/:/rootfs:ro \
  --volume=/var/run:/var/run:ro \
  --volume=/sys:/sys:ro \
  --volume=/var/lib/docker/:/var/lib/docker:ro \
  --volume=/dev/disk/:/dev/disk:ro \
  --publish=8080:8080 \
  --detach=true \
  --name=cadvisor \
  gcr.io/google-containers/cadvisor:$VERSION </code>
  
cAdvisor is now running (in the background) on http://localhost:8080. The setup includes directories with Docker state cAdvisor needs to observe.

To run Jaege agent (we cloned the jaeger from it's repository in script):<br/>
<code> $ cd jaeger-1.17.1-linux-amd64/ </code>
<code> $ ./jaeger-all-in-one </code><br/>
Now it's listeniing on port 16686.

To know more about the pumba check the following website:
https://www.gremlin.com/chaos-monkey/chaos-monkey-alternatives/docker/

## Create a Kubernetes Cluster on Ubuntu
The purpose of this part is to enable you to run a demo microservices application on a kubernetes cluster you have created. We used the tutorial from this url:<br/>
https://www.gremlin.com/community/tutorials/how-to-create-a-kubernetes-cluster-on-ubuntu-16-04-with-kubeadm-and-weave-net/ <br/>
test_environment.md indicates the steps to run the test environment.<br/>



