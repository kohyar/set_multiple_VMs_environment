# Setting up multiple VMs on GUI-less virtualbox
To set up multiple VMs on GUI-less virtualbox we followed these steps:
## Install Virtualbox 6.0
Using the installVBOX script you can install virtualbox 6.0 and virtualbox-ext-pack. It also tests if the ext-pack is installed or not:
<code>$ bash ./installVBOX </code>

To uninstall virtual box:
<code>$ sudo apt remove virtualbox virtualbox-6.0 </code>

## Installing virtual machines
The first step is to copy cloned VM into the host. Then you should register the VM in the VirtualBox:
<code> $ VBoxManage registervm ~/VirtualBox\ VMs/ububtu/ububtu.vbox </code>
To check if it is registerd:
<code>$ VBoxManage list vms </code>
The next step is cloning some virtual machines. To do this we use:
<code>$ bash ./CloneVMs </code>

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








