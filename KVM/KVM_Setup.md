# Set up VM using kvm
* Install KVM and its required packages:<br/>
<code>sudo apt update </code><br/>
<code>sudo apt install qemu qemu-kvm libvirt-bin  bridge-utils  virt-manager</code><br/>
* Start & enable libvirtd service:
<code>sudo service libvirtd start</code><br/>
<code>sudo update-rc.d libvirtd enable</code><br/>
Now verify the status of libvirtd service using below command,
<code>ervice libvirtd status</code><br/>
To check the version of KVM:
<code>kvm --version</code><br/>


## KVM commands
Find ip of geusts:Steps to find the ip address of Linux KVM guest virtual machine<br/>
    1. Open the terminal app or login using ssh to host server<br/>
    2. Get the network list: <code>virsh net-list</code><br/>
    3. Type the command: <code>virsh net-dhcp-leases networkNameHere</code><br/>

Type the following command to list network:<br/>
<code>virsh net-list</code><br/>
<code>virsh net-info default</code><br/>
<code>virsh net-dhcp-leases default</code><br/>

list of Vms:<br/>
<code>virsh list –all</code><br/>

List Running VMS
<code>virsh list</code><br/>


start VM:<br/>
<code>virsh start name</code><br/>


Turn of:<br/>
<code>virsh shutdown</code><br/>

Forcefully Stop A Guest<br/>
<code>virsh list</code><br/>
<code>virsh destroy domainName</code><br/>

suspend:<br/>
<code>virsh suspend guest1</code><br/>

reset:<br/>
<code>virsh reset guest1</code><br/>

To delete a VM Guest with virsh run:<br/>
<code>virsh undefine VM_NAME</code><br/>

## How to clone existing KVM virtual machine images on Linux:
<code>virt-clone --original {Domain-Vm-Name-Here} --name {New-Domain-Vm-Name-Here} –auto-clone</code><br/>
or:<br/>
<code>virt-clone --original {Domain-Vm-Name-Here} --name {New-Domain-Vm-Name-Here} --file {/var/lib/libvirt/images/File.Name.here}</code><br/>

## Move Guest to Another Host
On the Old Host (kvm01)<br/>
<code>virsh shutdown vm</code><br/>
<code>virsh dumpxml vm > /tmp/vm.xml</code><br/>
<code>scp /tmp/vm.xml kvm02:/tmp/vm.xml</code><br/>
<code>scp /var/lib/libvirt/images/vm.qcow2 kvm02:/var/lib/libvirt/images/vm.qcow2</code><br/>

On the New Host (kvm02)<br/>
<code>virsh define /tmp/vm.xml</code><br/>
<code>Domain vm defined from /tmp/vm.xml</code><br/>
<code>virsh start vm</code><br/>

Then activate the default network:<br/>
<code>virsh net-start default</code><br/>
If an error occured use the following link:<br/>
https://www.linuxtechi.com/install-configure-kvm-ubuntu-18-04-server/
    
Also you should change the Network Interface and the location of image file in xml file:<br/>
<code>virsh edit generic</code><br/>
Now you can start the vm.


## Install minikube and kubectl 
On server:
install Minikube and kubectl using following link:<br/>
https://computingforgeeks.com/how-to-run-minikube-on-kvm/ <br/>
You may need to set KVM as default driver:
<code>$  minikube config set vm-driver kvm2 </code><br/>
More info:<br/>
https://linuxhint.com/install-minikube-ubuntu/ <br/>

# Test Application
Then we can test the following example:<br/>
https://kubernetes.io/blog/2019/07/23/get-started-with-kubernetes-using-python/ <br/>

 
