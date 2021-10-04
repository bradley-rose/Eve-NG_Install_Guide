# Installation Guide for Eve-NG

- [Installation Guide for Eve-NG](#installation-guide-for-eve-ng)
  - [Prerequisites](#prerequisites)
    - [Official Documentation Resources](#official-documentation-resources)
    - [Video Resources](#video-resources)
    - [Hypervisor Installation](#hypervisor-installation)
    - [Obtain Network Appliance Images](#obtain-network-appliance-images)
  - [Installing the Eve-NG Virtual Machine](#installing-the-eve-ng-virtual-machine)
    - [Useful Video Tutorials](#useful-video-tutorials)
    - [Installation Guide](#installation-guide)
  - [Installing Network Appliance Images](#installing-network-appliance-images)
    - [Official Documentation Resources](#official-documentation-resources-1)
    - [Helpful Video Tutorial](#helpful-video-tutorial)
    - [Prerequisite Information](#prerequisite-information)
    - [VMDK Installation Guide](#vmdk-installation-guide)
    - [QCOW2 Installation Guide](#qcow2-installation-guide)

## Prerequisites
### Official Documentation Resources
1. [The primary documentation homepage](https://www.eve-ng.net/index.php/documentation/)
2. [General system requirements](https://www.eve-ng.net/index.php/documentation/installation/system-requirement/)

### Video Resources
1. [Eve-NG Installation Guide by David Bombal](https://www.youtube.com/watch?v=FDbgTlr-tnw)
2. [Adding Cisco Images to Eve-NG by David Bombal](https://www.youtube.com/watch?v=YKYdq3Ww_C0&t=0s)

### Hypervisor Installation
As with any bit of virtualization, you must have some form of hypervisor on your machine. A large note here though:  
**Oracle VirtualBox does NOT work!**  
Eve-NG specifically notes that in the [System Requirements](https://www.eve-ng.net/index.php/documentation/installation/system-requirement/) page.

Recommended Hypervisors: 
- [VMware Player](https://www.vmware.com/products/workstation-player.html) (**FREE!**)
- [VMware Workstation](https://www.vmware.com/products/workstation-pro.html)
- [Hyper-V](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v) (**FREE!**)
- [VMware ESXi](https://my.vmware.com/en/web/vmware/evalcenter?p=free-esxi7) (**FREE TIER AVAILABLE!**) (This is a Type-1 Hypervisor meant for bare-metal architecture on server hardware)

### Obtain Network Appliance Images
- [Cisco VIRL](https://learningnetworkstore.cisco.com/cisco-modeling-labs-personal/cisco-cml-personal)
- Google is your friend!

For $200 USD, you can purchase access to Cisco's Virtual Internet Routing Lab and resources. Once purchased, you can obtain **all** of the available images for use.  
If $200 USD is not in your budget, make excellent use of your web search skills. There are individuals out there who have publically uploaded their Cisco images. I cannot speak on the legality of obtaining and using these images, but all I'll say here is that they do exist.

## Installing the Eve-NG Virtual Machine

### Useful Video Tutorials
1. [Data Knox](https://www.youtube.com/watch?v=y391y1pCDe0)
2. [David Bombal](https://www.youtube.com/watch?v=FDbgTlr-tnw)

### Installation Guide
1. [Download the Eve-NG Community Edition Virtual Machine!](https://www.eve-ng.net/index.php/download/) I've had excellent success so far with using the pre-packaged OVF file, so I would recommend going this route as well. They also conveniently provide the ISO image should you choose to build and deploy your own virtual machine.
2. Extract the `.zip` to the `.ovf`.
3.  Deploy the virtual machine in your hypervisor of choice. If you've downloaded the `.ovf`, you want to "Open" an existing virtual machine, not create a new one. (`Ctrl+O`)
4. Adjust the virtual machine's resources according to your machine. At a **minimum**, the system requirements are:  
- **RAM**: 8GB
- **Processors**: 2

**Network Adapter**:  
- If you're operating on a wireless network, choose NAT.
- If you're operating on a wired Ethernet connection, choose Bridged.

5. Power it up!
The default credentials on first boot are:  

Username | Password
--- | ---
root | eve

  a. Create a new root password.  
  b. Leave the default hostname.  
  c. Leave the default domain name.  
  d. Leave the machine on DHCP unless you'd prefer it to hold a static IP address on your network. 
  e. Leave the NTP server blank.  
  f. Select *"direct connection"*.  

6. The machine will restart and display an IP address in the CLI. Open a web-browser and visit that IP address!  

The default credentials for the web-interface are: 

Username | Password | Console
--- | --- | ---
admin | eve | HTML5

Congratulations! You've officially installed and signed in to Eve-NG!

7. Next, [watch this video from this specific time-code](https://youtu.be/FDbgTlr-tnw?t=978) and play around with the interface! The main dashboard is the area where you'll have your list of labs! Create a new test lab, and get familiar with interacting with it. 

## Installing Network Appliance Images

### Official Documentation Resources
1. [QEMU Image Naming Table](https://www.eve-ng.net/index.php/documentation/qemu-image-namings/)
2. [Installing QCOW2 or VMDK Appliance Images](https://www.eve-ng.net/index.php/documentation/howtos/howto-add-cisco-vios-from-virl/)

### Helpful Video Tutorial
[David Bombal](https://www.youtube.com/watch?v=YKYdq3Ww_C0)

### Prerequisite Information
1. Visit the [Obtain Network Appliance Images](#obtain-network-appliance-images) section for details on obtaining network appliance images.  
2. If you're running on Windows, download an SFTP client application. If you're running on Ubuntu, SFTP is directly supported through the Nautilus file explorer. Not sure about MacOS.
- [WinSCP](https://winscp.net/eng/download.php)
- [FileZilla](https://filezilla-project.org/download.php)

There are two types of network appliance images: 
1. VMDK
2. QCOW2

EVE-NG uses the QCOW2 format, but we are able to simply convert the VMDK image types to QCOW2 for use.

### VMDK Installation Guide
1. Take note of the **QEMU Folder Name** and the **QEMU Image .qcow Name** [from this table!](https://www.eve-ng.net/index.php/documentation/qemu-image-namings/)
2. On your Eve-NG virtual machine command-line interface, navigate to: 
```
cd /opt/unetlab/addons/qemu
```

3. Create a directory for your respective image. For example, if we're uploading a layer-2 Switch IOSv, our directory name must begin with "`viosl2-`" as per the table linked above in step 1. **The directory name should match the image file name.** If your layer-2 switch image filename is `vios_l2-adventerprisek9-m.vmdk.SSA.153.vmdk`, then your corresponding action will be: 
```
mkdir viosl2-adventerprisek9-m.vmdk.SSA.153
```
**Note**: The underscore has been removed to ensure the directory name matches the table's listing, and the file extension has been removed. The remainder is left unchanged.

4. Upload your VMDK image file to the inside of this directory using the SFTP client downladed earlier. 
5. Convert the VMDK image to a QCOW2 image by executing the following from within the Eve-NG virtual machine CLI: 
```
/opt/qemu/bin/qemu-img convert -f vmdk -O qcow2 viosl2-adventerprisek9-m.vmdk.SSA.153.vmdk <QEMU Image .qcow Name>
```  
**Note**: The `<QEMU Image .qcow Name>` variable should be replaced with the applicable file name as per the table in Step 1. In this case of the layer-2 switch, it would be `virtioa.qcow2`.  

6. Delete the VMDK file. **Leave the QCOW2 file.**
7. Fix the file permissions. This must be applied after each image is uploaded. 
```
/opt/unetlab/wrappers/unl_wrapper -a fixpermissions
```

### QCOW2 Installation Guide
1. Take note of the **QEMU Folder Name** and the **QEMU Image .qcow Name** [from this table!](https://www.eve-ng.net/index.php/documentation/qemu-image-namings/)
2. On your Eve-NG virtual machine command-line interface, navigate to: 
```
cd /opt/unetlab/addons/qemu
```

3. Create a directory for your respective image. For example, if we're uploading a layer-2 Switch IOSv, our directory name must begin with "`viosl2-`" as per the table linked above in step 1. **The directory name should match the image file name.** If your layer-2 switch image filename is `vios_l2-adventerprisek9-m.vmdk.SSA.153.vmdk`, then your corresponding action will be: 
```
mkdir viosl2-adventerprisek9-m.vmdk.SSA.153
```
**Note**: The underscore has been removed to ensure the directory name matches the table's listing, and the file extension has been removed. The remainder is left unchanged.

4. Upload your QCOW2 image file to the inside of this directory using the SFTP client downladed earlier. 
5. Rename your QCOW2 image file to the applicable file name as per the table in Step 1. In this case of the layer-2 switch, it would be `virtioa.qcow2`.
6. Fix the file permissions. This must be applied after each image is uploaded. 
```
/opt/unetlab/wrappers/unl_wrapper -a fixpermissions
```