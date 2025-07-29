# 🧰 Installing VirtualBox on Ubuntu (From Official Site)

I installed **VirtualBox version 7.0.26r168464** by downloading the `.deb` package directly from the official Oracle VirtualBox website.

### Installation Steps:

1. **Go to the official download page**  
   👉 [https://www.virtualbox.org/wiki/Linux_Downloads](https://www.virtualbox.org/wiki/Linux_Downloads)

2. **Download the Debian package** for your Ubuntu version (e.g., `Ubuntu 20.04`, `22.04`, etc.)

3. **Install the package using your terminal**
   ```bash
   cd ~/Downloads
   sudo dpkg -i virtualbox-7.0_*.deb

4. **Fix any missing dependencies (if needed)**
   ```bash
   sudo apt --fix-broken install

5. **Verify the installation**
   ```bash
   virtualbox --help

VirtualBox is now ready for use. I use it to run virtual machines as part of my cybersecurity homelab setup.
   ```
   ✅ Version installed: VirtualBox 7.0.26r168464 on Ubuntu Linux
   ```
---
## Host Key in VirtualBox

The **Host Key** is a special key (typically the **Right CTRL**) that lets you interact with VirtualBox instead of the guest operating system inside the virtual machine (VM). It's used to exit the VM and return to the host system.

### Default Host Key:

- The default is usually the **Right CTRL** key, but it may vary based on your system or preferences.

**Purpose:**

The Host Key allows you to:

**1. Release Input:** If the VM has captured your keyboard or mouse, pressing the Host Key returns control to the host system.

**2. Access VirtualBox Features:** Use key combinations to perform actions like switching to full-screen, capturing screenshots, or opening the VirtualBox menu.

To check your current Host Key, go to **File ➔ Preferences** in VirtualBox.

![Preferences](imgs/preferences.jpg)

Go to **Input ➔ Host Key Combination** to view or change the Host Key. To set a new key, select the box and press the desired key on your keyboard.

![Host Key](imgs/hostkey.jpg)

---
**Set Up a New NAT Network in VirtualBox**

We’ll use a NAT Network to connect Virtual Machines (VMs) to each other and the internet.

1. Open VirtualBox.
2. Go to **File ➔ Tools ➔ Network Manager**.
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

* **Windows Server 2025**: I found and downloaded the evaluation ISO.
* **Windows 11 Enterprise**: I downloaded this through my Microsoft account.
* **Ubuntu 24.04 Desktop**: I downloaded it from the [Ubuntu Official Site](https://ubuntu.com/download/desktop).
* **Ubuntu Server 24.04**: I also got this from the [Ubuntu Official Site](https://ubuntu.com/download/server).
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
## Enable Full Screen with VirtualBox Guest Additions

By default, VirtualBox virtual machines don’t run in full screen. To enable it, you can install **VirtualBox Guest Additions**, a set of drivers and system tools that improve VM performance and usability.

**For Windows 10/11:**

With the virtual machine running, go to the menu bar and select **Devices ➔ Insert Guest Additions CD image…**. This will mount the installer inside the VM. Follow the prompts to complete the installation.

![Guest Additions](imgs/vga.jpg)

Open the **File Explorer** in the Windows virtual machine. Navigate to **This PC**, then double-click the **VirtualBox Guest Additions** drive to open it.

![Guest Additions](imgs/vga1.jpg)

Inside the VirtualBox Guest Additions folder, you’ll see several executable files. Double-click the generic VBoxWindowsAdditions program to start the installation.

![Guest Additions](imgs/vga2.jpg)

Follow the default installation wizard settings.

![Guest Additions](imgs/vga3.jpg)

Choose to "Reboot Now".

![Guest Additions](imgs/vga4.jpg)

Allow the Virtual Machine to restart.

You should now be able to make the machine full screen. 

**For Linux - 🐧 Ubuntu & Kali Linux VMs**

- After inserting the CD, open the file manager and run:  
 `VBoxLinuxAdditions.run`

> 📸 **(Right-click → Open in Terminal → Run with sudo if needed)** ![Open in Terminal](img/vgalinux.png)

> 📸 ![Terminal](img/vgalinux1.png)

     ```bash
     sudo ./VBoxLinuxAdditions.run

- You may need to install required packages beforehand:
     ```bash
     sudo apt update
     sudo apt install -y build-essential dkms linux-headers-$(uname -r)

- Reboot the VM after installation.

✅ Result

Once Guest Additions are installed and integration options are enabled:

- VMs can enter full-screen mode seamlessly.
- Clipboard and drag-and-drop work both ways between host and guest.
