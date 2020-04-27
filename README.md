# Setting up multiple VMs on GUI-less virtualbox
Some useful references to know more about microservices:
 * https://www.nginx.com/blog/deploying-microservices/

To set up multiple VMs on GUI-less virtualbox we followed these steps:
## Install Virtualbox 6.0
Using the installVBOX script you can install virtualbox 6.0 and virtualbox-ext-pack. It also tests if the ext-pack is installed or not:
<code>$ bash ./installVBOX </code>

To uninstall virtual box:<br/>
<code>$ sudo apt remove virtualbox virtualbox-6.0 </code><br/>
or:<br/>
<code> $ sudo apt-get remove virtualbox* --purge </code><br/>

## Install the first VM
After setting up an ubuntu virtual machine we run the <code>VMRequirement</code> script to install required following packages:<br/>
* Install npm on guest
* Install Python2 &3 on guest
* Install Pumba on guest
* Install Stress on guest
* Install cAdvisor on guest
* Install Docker and Docker compass on guest
* Install Jaeger on guest
* Install npm on guest
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

## Move the VM to the server
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

Other option to move the vm is to copy the cloned VM into the host. Then you should register the VM in the VirtualBox:<br/>
<code> $ VBoxManage registervm ~/VirtualBox\ VMs/machineName/machineName.vbox </code>

To check if it is registerd:<br/>
<code>$ VBoxManage list vms </code>

Configure VM settings:<br/> 
<code>$ VBoxManage modifyvm vmtest --ostype  "Linux26_64" --memory 4096 --acpi on --cpus 1  --description guestname </code>

## Duplicate the VM
The next step is cloning some virtual machines. To do this we use:
<code>$ bash ./CloneVMs </code>

## 

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
To start all VMs and find IP of them we use the following command:
<code> $ bash ./FindAllIPsScript</code>








