# 🧰 Installing VMware Fusion on Mac

This guide walks you through the easy steps to download and install **VMware Fusion** on your Mac.

---

## ✅ Step 1: Download VMware Fusion

1. Open your web browser and go to the [official VMware Fusion page](https://www.vmware.com/products/fusion.html).  
2. Click **Download Now** or **Try Now** to download the latest version for macOS.  
3. Save the installer file (usually a `.dmg`) to your computer.

---

## ✅ Step 2: Install VMware Fusion

1. Open the downloaded `.dmg` file by double-clicking it.  
2. In the window that appears, double-click the VMware Fusion installer icon.  
3. Follow the on-screen instructions to complete the installation. You might need to enter your Mac’s password and approve security permissions.

---

## 🎉 You're Done!

VMware Fusion is now installed and ready for creating and running virtual machines on your Mac.

---

**Set Up a New NAT Network in VirtualBox**

We’ll use a NAT Network to connect Virtual Machines (VMs) to each other and the internet.

1. Open VirtualBox.
2. Go to **Tools ➔ Network Manager**.
3. Create a new NAT Network.

![Nat Network](imgs/natnetwork1.jpg)

Select NAT Networks ➔ “Create”. 

![Nat Network](imgs/natnetwork2.jpg)

At the bottom, name the NatNetwork `skynet-network` and choose an IPv4 prefix, refer to the Project Overview guide for more detail on IPv4 prefixes. Select “Apply” to save changes. Set the **IPv4 Prefix** to `10.0.0.0/24`.
8. Enable the **DHCP** option to allow automatic IP assignment.
9. Click **Apply** to save the configuration.

![Nat Network](imgs/natnetwork3.png)

### Outcome:

This process created a NAT network named `skynet-network` with the subnet `10.0.0.0/24`. DHCP is enabled, meaning any virtual machines connected to this network will automatically receive an IP address.

> 💡 **Note**: By default, the `skynet-network` NAT Network will be selected for all newly provisioned Virtual Machines.

---

### Downloaded ISOs

I made sure to get the official installation ISO files for each operating system:

* **Windows Server 2022**: I found and downloaded the evaluation ISO.
* **Windows 10 Enterprise LTSC**: I downloaded this through my Microsoft account.
* **Ubuntu 22.04 Desktop**: I downloaded it from the [Ubuntu Official Site](https://ubuntu.com/download/desktop).
* **Ubuntu Server 22.04**: I also got this from the [Ubuntu Official Site](https://ubuntu.com/download/server).
* **Security Onion**: I downloaded the ISO from the [Security Onion Official Site](https://securityonionsolutions.com/download/).
* **Kali Linux 2024**: I chose the "Installer Images" option from the [Kali Linux Official Site](https://www.kali.org/get-kali/#kali-virtual-machines) for a clean install.

---

## Create A New Virtual Machine

Navigate to VirtualBox. Go to Machine ➔ New.

![New VM](imgs/newvm.jpg)

Enter a name for the Virtual Machine.

Choose default Folder location.

Select “Type: Microsoft Windows”. Version: “Windows Server 2025 (64-bit)” 

![New VM](imgs/newvm1.png)

**Set Hardware Specifications**

Each virtual machine should have at least **4 GB of RAM (4096 MB)** and **2 CPUs**, unless stated otherwise.

> 💡 **Note**: 👉 Refer to the “Project Overview” guide for more information on default VM settings and names.

For Windows 11: Enable EFI.

![New VM](imgs/newvm2.png)

Created a **dynamically allocated** virtual hard disk (unchecked “Pre-allocate”) with **50 GB** space.

![New VM](imgs/newvm3.png)

Review specifications. Select “Finish”. 

![New VM](imgs/newvm4.jpg)

### Attach ISO and Configure Network

Select the newly created virtual machine and open Settings. Under the Storage tab, click the Empty optical drive and choose Choose a disk file…. Locate your downloaded ISO file (typically in the Downloads folder) and click Open.

Next, go to the Network tab. Set Attached to as NAT Network, and choose skynet network in the Name dropdown. Click OK to apply the changes.

![Nat Network](imgs/natnetwork4.png)

Select the Virtual Machine, then Select “Start”.


When the virtual machine starts, you'll see a prompt to press a key. Press any letter key to begin the operating system’s installation wizard.

![Boot](imgs/boot.jpg)

---
## 📸 Virtual Machine Snapshot

A snapshot saves the exact state of a virtual machine at a specific point in time, including its disk, memory, and hardware settings. This allows you to revert back to that state if needed.

In VirtualBox, select the virtual machine, then click Take to create a snapshot.

![Snapshots](imgs/snapshots.png)
![Snapshots](imgs/snapshot1.jpg)

Title the snapshot with something descriptive so you can recall what configurations were made up until this point.

#### Benefits of Taking Snapshots:
- 🛠️ **Experiment Safely**: Allows me to experiment with configurations without worrying about breaking the system.
- 🔄 **Easy Reverts**: If something goes wrong, I can easily revert to a previously saved state.
- ⏳ **Avoid Starting Over**: No need to start from scratch if mistakes happen snapshots help restore functionality quickly.

Using snapshots makes the setup process more efficient, recoverable, and flexible, allowing for smooth and controlled changes throughout the project.

---
