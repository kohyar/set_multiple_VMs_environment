# Setting up multiple VMs on GUI-less virtualbox
Some useful references to know more about microservices:
 * https://www.nginx.com/blog/deploying-microservices/

To set up multiple VMs on GUI-less virtualbox we followed these steps:
## Install Virtualbox 6.0
Using the installVBOX script you can install virtualbox 6.0 and virtualbox-ext-pack. It also tests if the ext-pack is installed or not:
<code>$ bash ./installVBOX </code>

To uninstall virtual box:<br/>
<code>$ sudo apt remove virtualbox virtualbox-6.0 </code>

## Install the first VM
After setting up an ubuntu virtual machine we should run the following command to install required packages:<br/>
<code>$ bash ./VMRequirement</code>

The we install cAdvisor. First clone the cAdvisor from it's repository:<br/>
<code>$ git clone https://github.com/google/cadvisor.git </code>

Running cAdvisor in a Docker Container:<br/>
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

We set up an ubuntu guest on our local machine, then we copy exported machin to the destiation:<br/>
<code> $ vboxmanage export machineName -o test.ova</code><br/>
<code> $ vboxmanage import test.ova</code>

We set the bridge network again after importing the ova file. To create the bridge interface in host os:<br/>
<code>$ brctl addbr vmtestbr1 </code><br/>
<code>$ ifconfig  vmtestbr1 192.168.222.1  netmask 255.255.255.0 up </code><br/>
<code>$ ping -c 2 192.168.222.1 </code>

Declare a bridge interface:<br/> 
<code>$ VBoxManage modifyvm guestname --nic1 bridged --nictype1 82545EM --bridgeadapter1 vmtestbr1 </code>

VRDE is for access via rdp client:<br/>
<code>$ VBoxManage modifyvm guestname --vrde on </code>

## Duplicate the VM
The next step is cloning some virtual machines. To do this we use:
<code>$ bash ./CloneVMs </code>

## Other option to move a vm
The first step is to copy cloned VM into the host. Then you should register the VM in the VirtualBox:<br/>
<code> $ VBoxManage registervm ~/VirtualBox\ VMs/ububtu/ububtu.vbox </code>

To check if it is registerd:<br/>
<code>$ VBoxManage list vms </code>

Configure VM settings:<br/> 
<code>$ VBoxManage modifyvm vmtest --ostype  "Linux26_64" --memory 4096 --acpi on --cpus 1  --description guestname </code>

## Headless run of machines
Using the following command you can run a guest machin:
<code>$ VBoxManage startvm guestName --type headless </code>

List all available virtual machines:
<code>$ VBoxManage list vms </code>

List all running available virtual machines:
<code> $ VBoxManage list runningvms</code>

## Find IP of a guest
To find IP of a guest use the following command:
<code> $ bash ./FindIPScript guestName</code>








