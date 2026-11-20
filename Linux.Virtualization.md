
# VMware ESX

VMware ESX (also known as ESXi, and renamed back to ESX starting in version 9.0) is a type-1 bare-metal hypervisor developed by VMware (a Broadcom subsidiary) that runs directly on server hardware to host multiple virtual machines. [1] (https://en.wikipedia.org/wiki/VMware_ESX), [2] (https://endoflife.date/esxi), [3] (https://www.starwindsoftware.com/blog/esx-vs-esxi-vmware-hypervisors-compared/)

Key Characteristics

• Architecture: Built around the vmkernel microkernel, which directly schedules CPU, memory, storage, and network resources for virtual machines. [1] (https://www.pluralsight.com/resources/blog/tech-operations/what-is-vmware-esx-server-and-why-you-need-it), [2] (https://en.wikipedia.org/wiki/VMware_ESX)
• Footprint & Evolution: Early ESX versions relied on a Linux-based Service Console (deprecated in version 4.1). ESXi removed that console for a smaller, more secure footprint, and Broadcom brought back the ESX name with version 9.0. [1] (https://www.reddit.com/r/sysadmin/comments/xryri/can_someone_please_explain_what_the_hell_esx_esxi/), [2] (https://en.wikipedia.org/wiki/VMware_ESX)
• Ecosystem: Typically managed through VMware vCenter and vSphere alongside features like vMotion and vSAN. [1] (https://knowledge.broadcom.com/external/article/316595/build-numbers-and-versions-of-vmware-esx.html), [2] (https://en.wikipedia.org/wiki/VMware_ESX)

Current Versions & Support

Per Broadcom's build documentation and endoflife.date:
• ESX 9.1: Active release (e.g., 9.1.1.0100); general support runs until August 12, 2028. [1] (https://endoflife.date/esxi), [2] (https://knowledge.broadcom.com/external/article/316595/build-numbers-and-versions-of-vmware-esx.html)
• ESX 9.0: Active release (e.g., 9.0.2.0100); general support runs until September 17, 2027. [1] (https://knowledge.broadcom.com/external/article/316595/build-numbers-and-versions-of-vmware-esx.html), [2] (https://endoflife.date/esxi)
• ESXi 8.0: Active release (e.g., 8.0 Update 3k); general support runs until October 11, 2027. [1] (https://knowledge.broadcom.com/external/article/316595/build-numbers-and-versions-of-vmware-esx.html), [2] (https://endoflife.date/esxi)
• ESXi 7.0 & older: General support for ESXi 7.0 ended on October 2, 2025. [1] (https://www.lansweeper.com/blog/eol/vmware-esxi-end-of-life/), [2] (https://endoflife.date/esxi)

---

# KVM Linux

Kernel-based Virtual Machine (KVM) is an open-source virtualization module built into the Linux kernel that turns Linux into a hypervisor for running virtual machines (VMs) with near-native performance. Merged into mainline Linux in version 2.6.20 (February 5, 2007), it relies on CPU hardware virtualization extensions such as Intel VT (vmx) or AMD-V (svm). [1] (https://en.wikipedia.org/wiki/Kernel-based_Virtual_Machine), [2] (https://www.redhat.com/en/topics/virtualization/what-is-KVM), [3] (https://www.youtube.com/watch?v=mAZNlyXVoT4), [4] (https://wiki.archlinux.org/title/KVM)

How It Works

• Kernel module (kvm.ko): Exposes the /dev/kvm interface and pairs with processor-specific modules (kvm-intel.ko or kvm-amd.ko) to manage guest memory and direct CPU execution. [1] (https://linux-kvm.org/page/Main_Page), [2] (https://www.youtube.com/watch?v=Cz3Pi11Tr84&t=596), [3] (https://en.wikipedia.org/wiki/Kernel-based_Virtual_Machine)
• Linux processes: Each VM runs as a standard Linux process scheduled and isolated by the kernel (often reinforced with SELinux/sVirt). [1] (https://www.redhat.com/en/topics/virtualization/what-is-KVM)
• User-space tools: KVM handles CPU and memory virtualization rather than full device emulation, so it typically pairs with QEMU (or lightweight VMMs like Firecracker or kvmtool) to emulate hardware and manage I/O via paravirtualized virtio drivers. [1] (https://wiki.archlinux.org/title/KVM), [2] (https://linux-kvm.org/page/Main_Page), [3] (https://en.wikipedia.org/wiki/Kernel-based_Virtual_Machine)
• Management layer: Tools like libvirt (virsh, virt-install), Virtual Machine Manager (virt-manager), or Cockpit simplify creating and controlling VMs. [1] (https://virt-manager.org/), [2] (https://www.youtube.com/watch?v=mAZNlyXVoT4), [3] (https://www.redhat.com/en/topics/virtualization/what-is-KVM)
Most users on r/kernel agree that KVM acts like a hybrid ("type 1.5") hypervisor because the core hypervisor runs in the bare-metal Linux kernel while user-space components like QEMU handle device emulation and VM management. [1] (https://www.reddit.com/r/kernel/comments/1amt9u3/what_is_kvm_how_can_a_hypervisor_be_built_into_a/)

Quick Hardware & Module Check

Run these commands on your Linux host to verify support: [1] (https://docs.oracle.com/en/learn/ol-kvm/index.html)
bash
lscpu | grep -i virtualization
lsmod | grep kvm
Use code with caution.
If virtualization is missing, check your system firmware/BIOS to ensure Intel VT-x or AMD-V is enabled. For broader architectural context, see Red Hat's KVM overview or the Kernel-based Virtual Machine entry on Wikipedia. [1] (https://wiki.archlinux.org/title/KVM), [2] (https://www.youtube.com/watch?v=mAZNlyXVoT4), [3] (https://www.redhat.com/en/topics/virtualization/what-is-KVM), [4] (https://en.wikipedia.org/wiki/Kernel-based_Virtual_Machine)

---

# [Proxmox](https://www.proxmox.com/en/)  

---

# Azure Virtual Desktop (AVD)

Azure Virtual Desktop (AVD) is Microsoft's cloud-based Virtual Desktop Infrastructure (VDI) and Desktop-as-a-Service (DaaS) platform that delivers Windows 11, Windows 10, and Windows Server desktops and apps from Azure. Microsoft manages the control plane (gateway, broker, diagnostics, load balancing), while you manage the session host virtual machines, networking, storage, and user access. [1] (https://azure.microsoft.com/en-gb/products/virtual-desktop), [2] (https://learn.microsoft.com/en-us/azure/virtual-desktop/overview), [3] (https://getnerdio.com/azure-vdi/), [4] (https://www.youtube.com/watch?v=aPEibGMvxZw&t=2)

Key Capabilities

• Single- & Multi-Session: Run dedicated personal desktops or shared multi-session Windows 10/11 Enterprise and Windows Server VMs to reduce VM count and cost. [1] (https://learn.microsoft.com/en-us/azure/virtual-desktop/overview), [2] (https://getnerdio.com/azure-vdi/)
• Full Desktops or RemoteApp: Deliver complete virtual desktops or stream individual applications (Win32, MSIX, Appx). [1] (https://learn.microsoft.com/en-us/azure/virtual-desktop/overview)
• Hybrid & On-Premises: Extend management to on-premises infrastructure using Azure Virtual Desktop Hybrid or Azure Virtual Desktop for Azure Local. [1] (https://azure.microsoft.com/en-us/pricing/details/virtual-desktop/), [2] (https://learn.microsoft.com/en-us/azure/virtual-desktop/overview)
• Cost & Profile Controls: Use autoscale to power VMs up or down on schedules or demand, and FSLogix profile containers to roam user profiles smoothly across pooled hosts. [1] (https://www.youtube.com/watch?v=g4gxvCOqHtk), [2] (https://learn.microsoft.com/en-us/azure/virtual-desktop/overview)
• Client Access: Connect via the Windows App or supported clients across Windows, macOS, iOS, Android, and web browsers. [1] (https://learn.microsoft.com/en-us/azure/virtual-desktop/), [2] (https://en.wikipedia.org/wiki/Azure_Virtual_Desktop), [3] (https://learn.microsoft.com/en-us/previous-versions/remote-desktop-client/connect-windows-cloud-services)

Licensing & Costs

• User Licensing (BYOL): Often covered at no extra desktop licensing cost if users hold eligible Microsoft 365 (such as Business Premium, E3/E5, F3, A3/A5), Windows Enterprise/Education per-user licenses, or qualifying RDS CALs/SALs with Software Assurance for Windows Server. [1] (https://azure.microsoft.com/en-us/pricing/details/virtual-desktop/)
• Infrastructure Costs: You pay for underlying Azure VMs, OS/data/profile storage, and networking—typically pay-as-you-go or Reserved Instances. On Reddit's r/AZURE, opinions on AVD costs are mixed: many report strong savings over traditional on-premises RDS or Citrix when paired with autoscaling and right-sized SKUs, while others note higher-than-expected costs without careful planning and ongoing management. [1] (https://www.reddit.com/r/AZURE/comments/1gtg60p/anyone_tried_azure_virtual_desktop_wondering_if/), [2] (https://azure.microsoft.com/en-us/pricing/details/virtual-desktop/), [3] (https://www.youtube.com/watch?v=g4gxvCOqHtk)
Explore deployment options and rates on Azure Virtual Desktop or review the Azure Virtual Desktop Pricing details. [1] (https://azure.microsoft.com/en-gb/products/virtual-desktop), [2] (https://azure.microsoft.com/en-us/pricing/details/virtual-desktop/)

---

# Citrix VDI 

Citrix VDI (now part of Citrix DaaS and Citrix Virtual Apps and Desktops) is an enterprise virtualization platform that hosts complete Windows and Linux desktop environments and individual apps on centralized data centers to deliver them to any remote device. [1] (https://www.citrix.com/solutions/virtualization-vdi.html), [2] (https://www.apporto.com/what-is-citrix-vdi), [3] (https://www.venn.com/learn/citrix-vdi/)

How It Works

• Core Architecture: Central servers run desktop operating systems inside virtual machines (VMs) managed by a hypervisor. Connection brokers, like Delivery Controllers, link client requests to resource pools. [1] (https://www.citrix.com/glossary/what-is-vdi-virtual-desktop-infrastructure.html), [2] (https://www.venn.com/learn/citrix-vdi/)
• Access Clients: Users connect through the Citrix Workspace App or a web browser via NetScaler and StoreFront portals. [1] (https://www.youtube.com/watch?v=EE8fcFp68Cw&t=189), [2] (https://www.youtube.com/watch?v=xnheghil3ec&t=2)
• Deployment Types:
	• Persistent VDI: Gives users a dedicated desktop where personal files and changes are saved across sessions.
	• Non-Persistent VDI: Resets the desktop image back to a clean state every time the user logs out or restarts, which simplifies IT maintenance. [1] (https://www.citrix.com/glossary/what-is-vdi-virtual-desktop-infrastructure.html)

Key Benefits

• Centralized Management: IT administrators can manage software updates and security through single "golden images" rather than touching individual physical PCs. [1] (https://www.citrix.com/solutions/virtualization-vdi.html)
• Enhanced Security: Sensitive data remains locked inside the corporate data center or cloud, minimizing the risk of data theft if an endpoint device is lost or stolen. [1] (https://www.citrix.com/solutions/virtualization-vdi.html), [2] (https://www.citrix.com/glossary/what-is-vdi-virtual-desktop-infrastructure.html)
• High-Definition Experience: Uses HDX protocol technology to deliver smooth audio, video, 3D graphics, and Microsoft Teams optimizations over standard network connections. [1] (https://docs.citrix.com/en-us/citrix-virtual-apps-desktops/install-configure/server-vdi.html), [2] (https://www.youtube.com/watch?v=cJZ-Gdmq6Ow), [3] (https://www.citrix.com/solutions/virtualization-vdi.html)

---

# What is LVM in Linux?

In Linux, Logical Volume Manager (LVM) is a storage management framework that uses the kernel's device-mapper to create flexible "virtual partitions" instead of relying on fixed physical disk partitions. It acts as an abstraction layer between physical storage devices and file systems. [1] (https://www.reddit.com/r/linux4noobs/comments/8gvj0j/how_does_lvm_work_exactly/), [2] (https://en.wikipedia.org/wiki/Logical_Volume_Manager_(Linux)), [3] (https://wiki.archlinux.org/title/LVM)

Core Building Blocks

LVM organizes storage into three main layers, built from small blocks called extents (such as Physical Extents, or PEs): [1] (https://wiki.debian.org/LVM), [2] (https://wiki.archlinux.org/title/LVM)
• Physical Volumes (PV): Underlying storage devices such as hard drives, SSDs, partitions, or RAID arrays initialized for use with LVM.
• Volume Groups (VG): Pools of storage created by combining one or more Physical Volumes.
• Logical Volumes (LV): Virtual partitions carved out of a Volume Group that can be formatted with a file system (like ext4 or XFS) and mounted like standard partitions. [1] (https://ubuntu.com/server/docs/explanation/storage/about-lvm/), [2] (https://wiki.archlinux.org/title/LVM), [3] (https://wiki.debian.org/LVM)

Common Usage Examples & Benefits

• Dynamic resizing: Expand or shrink logical volumes without repartitioning disks.
• Spanning multiple disks: Grow a logical volume across multiple physical drives inside the same volume group.
• Snapshots: Capture point-in-time copies of a logical volume for consistent backups or safe system updates.
• Online disk migration: Move data between drives while the system is running using tools like pvmove.
• Basic setup workflow: Initialize a disk with pvcreate, group it with vgcreate, and carve out space with lvcreate. [1] (https://askubuntu.com/questions/3596/what-is-lvm-and-what-is-it-used-for), [2] (https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/configuring_and_managing_logical_volumes/overview-of-logical-volume-management_configuring-and-managing-logical-volumes), [3] (https://www.linuxjournal.com/content/lvm-demystified), [4] (https://wiki.archlinux.org/title/LVM), [5] (https://ubuntu.com/server/docs/explanation/storage/about-lvm/)
Most users in the Ask Ubuntu forum reach a consensus that dynamic resizing, spanning multiple disks, and taking snapshots are core benefits of LVM. Likewise, most users in the r/linux4noobs forum agree that LVM acts as an abstraction layer using extents for flexible, online storage management. For full technical details, see Logical Volume Manager (Linux) on Wikipedia. [1] (https://en.wikipedia.org/wiki/Logical_Volume_Manager_(Linux)), [2] (https://askubuntu.com/questions/3596/what-is-lvm-and-what-is-it-used-for), [3] (https://www.reddit.com/r/linux4noobs/comments/8gvj0j/how_does_lvm_work_exactly/)

Limitations & Alternatives

• No built-in redundancy: Standard LVM does not protect against drive failure on its own; losing a disk in a spanned setup can cause data loss unless paired with RAID. [1] (https://www.linuxjournal.com/content/lvm-demystified), [2] (https://wiki.archlinux.org/title/LVM)
• Added complexity: Setup and maintenance involve extra commands, metadata, and background services, and Windows does not natively read LVM partitions. [1] (https://wiki.archlinux.org/title/LVM)
• Related alternatives: Traditional disk partitioning (MBR/GPT), software RAID (mdadm), and integrated volume/file-system managers such as ZFS or Btrfs offer alternative approaches depending on your needs.


---

```
user@pbzitops01:~$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0    7:0    0  63.8M  1 loop /snap/core20/3015
loop1    7:1    0     4K  1 loop /snap/bare/5
loop2    7:2    0    74M  1 loop /snap/core22/3129
loop3    7:3    0  66.8M  1 loop /snap/core24/2307
loop4    7:4    0   285M  1 loop /snap/firefox/9171
loop5    7:5    0  12.7M  1 loop /snap/firmware-updater/262
loop6    7:6    0 531.5M  1 loop /snap/gnome-42-2204/263
loop7    7:7    0   616M  1 loop /snap/gnome-46-2404/177
loop8    7:8    0  91.7M  1 loop /snap/gtk-common-themes/1535
loop9    7:9    0   402M  1 loop /snap/mesa-2404/1839
loop10   7:10   0   2.7G  1 loop /snap/rider/834
loop11   7:11   0  11.7M  1 loop /snap/snap-store/1504
loop12   7:12   0  32.5M  1 loop /snap/snapd/28332
loop13   7:13   0   828K  1 loop /snap/snapd-desktop-integration/391
sda      8:0    0    70G  0 disk 
├─sda1   8:1    0     1M  0 part 
└─sda2   8:2    0    70G  0 part /
sr0     11:0    1  1024M  0 rom  
user@pbzitops01:~$ echo 1 | sudo tee /sys/class/block/sda/device/rescan
[sudo] password for user: 
1
user@pbzitops01:~$ lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
loop0    7:0    0  63.8M  1 loop /snap/core20/3015
loop1    7:1    0     4K  1 loop /snap/bare/5
loop2    7:2    0    74M  1 loop /snap/core22/3129
loop3    7:3    0  66.8M  1 loop /snap/core24/2307
loop4    7:4    0   285M  1 loop /snap/firefox/9171
loop5    7:5    0  12.7M  1 loop /snap/firmware-updater/262
loop6    7:6    0 531.5M  1 loop /snap/gnome-42-2204/263
loop7    7:7    0   616M  1 loop /snap/gnome-46-2404/177
loop8    7:8    0  91.7M  1 loop /snap/gtk-common-themes/1535
loop9    7:9    0   402M  1 loop /snap/mesa-2404/1839
loop10   7:10   0   2.7G  1 loop /snap/rider/834
loop11   7:11   0  11.7M  1 loop /snap/snap-store/1504
loop12   7:12   0  32.5M  1 loop /snap/snapd/28332
loop13   7:13   0   828K  1 loop /snap/snapd-desktop-integration/391
sda      8:0    0    90G  0 disk 
├─sda1   8:1    0     1M  0 part 
└─sda2   8:2    0    70G  0 part /
sr0     11:0    1  1024M  0 rom  
user@pbzitops01:~$ sudo parted /dev/sda
GNU Parted 3.6
Using /dev/sda
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) print                                                            
Warning: Not all of the space available to /dev/sda appears to be used, you can fix the GPT to use all of the space
(an extra 41943040 blocks) or continue with the current setting? 
Fix/Ignore? fix
Model: VMware Virtual disk (scsi)
Disk /dev/sda: 96.6GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 

Number  Start   End     Size    File system  Name  Flags
 1      1049kB  2097kB  1049kB                     bios_grub
 2      2097kB  75.2GB  75.2GB  ext4

(parted) resizepart 2 100%
Warning: Partition /dev/sda2 is being used. Are you sure you want to continue?
Yes/No? yes                                                               
(parted) print                                                            
Model: VMware Virtual disk (scsi)
Disk /dev/sda: 96.6GB
Sector size (logical/physical): 512B/512B
Partition Table: gpt
Disk Flags: 

Number  Start   End     Size    File system  Name  Flags
 1      1049kB  2097kB  1049kB                     bios_grub
 2      2097kB  96.6GB  96.6GB  ext4

(parted) quit                                                             
Information: You may need to update /etc/fstab.

user@pbzitops01:~$ df                                                     
Filesystem     1K-blocks     Used Available Use% Mounted on
tmpfs            1224244     2092   1222152   1% /run
/dev/sda2       71931084 52999936  15454724  78% /
tmpfs            6121204       84   6121120   1% /dev/shm
tmpfs               5120        0      5120   0% /run/lock
tmpfs            1224240      104   1224136   1% /run/user/120
tmpfs            1224240      128   1224112   1% /run/user/1000
user@pbzitops01:~$ sudo resize2fs /dev/sda2
resize2fs 1.47.0 (5-Feb-2023)
Filesystem at /dev/sda2 is mounted on /; on-line resizing required
old_desc_blocks = 9, new_desc_blocks = 12
The filesystem on /dev/sda2 is now 23592443 (4k) blocks long.

user@pbzitops01:~$ df
Filesystem     1K-blocks     Used Available Use% Mounted on
tmpfs            1224244     2092   1222152   1% /run
/dev/sda2       92569516 52999940  35254396  61% /
tmpfs            6121204       84   6121120   1% /dev/shm
tmpfs               5120        0      5120   0% /run/lock
tmpfs            1224240      104   1224136   1% /run/user/120
tmpfs            1224240      128   1224112   1% /run/user/1000
user@pbzitops01:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           1.2G  2.1M  1.2G   1% /run
/dev/sda2        89G   51G   34G  61% /
tmpfs           5.9G   84K  5.9G   1% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           1.2G  104K  1.2G   1% /run/user/120
tmpfs           1.2G  128K  1.2G   1% /run/user/1000
user@pbzitops01:~$ 

```