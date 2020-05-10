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

## How to clone existing KVM virtual machine images on Linux:
<code>virt-clone --original {Domain-Vm-Name-Here} --name {New-Domain-Vm-Name-Here} –auto-clone</code><br/>
or:
<code>virt-clone --original {Domain-Vm-Name-Here} --name {New-Domain-Vm-Name-Here} --file {/var/lib/libvirt/images/File.Name.here}</code><br/>


