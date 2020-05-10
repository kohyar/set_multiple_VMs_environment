# Set up VM using kvm
* Install KVM and its required packages:<br/>
<code>sudo apt update </code><br/>
<code>sudo apt install qemu qemu-kvm libvirt-bin  bridge-utils  virt-manager</code><br/>
*Start & enable libvirtd service:
<code>sudo service libvirtd start</code><br/>
<code>sudo update-rc.d libvirtd enable</code><br/>
Now verify the status of libvirtd service using below command,
<code>ervice libvirtd status</code><br/>
To check the version of KVM:
<code>kvm --version</code><br/>


## KVM commands
Find ip of geusts:Steps to find the ip address of Linux KVM guest virtual machine
    1. Open the terminal app or login using ssh to host server
    2. Get the network list: virsh net-list
    3. Type the command: virsh net-dhcp-leases networkNameHere

usually:
Type the following command to list network:
# virsh net-list
# virsh net-info default
# virsh net-dhcp-leases default

list of Vms:
virsh list –all

List Running VMS
Type the following command:
# virsh list


start VM:
virsh start name


Turn of:
virsh shutdown

Forcefully Stop A Guest
# virsh list
# virsh destroy domainName

suspend:
virsh suspend guest1

reset:
virsh reset guest1


How to clone existing KVM virtual machine images on Linux:
# virt-clone --original {Domain-Vm-Name-Here} --name {New-Domain-Vm-Name-Here} –auto-clone
or:
# virt-clone --original {Domain-Vm-Name-Here} --name {New-Domain-Vm-Name-Here} --file {/var/lib/libvirt/images/File.Name.here}


