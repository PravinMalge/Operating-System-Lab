# Practical 01: Installation of Linux (Ubuntu) using Oracle VM VirtualBox

## 🎯 Objective

To configure a virtual environment using Oracle VM VirtualBox, allocate system hardware resources, attach an ISO image, and successfully install the Ubuntu Linux operating system.

---

## 🛠️ Requirements & Tools

* **Hypervisor:** Oracle VM VirtualBox Manager
* **Operating System:** Ubuntu Linux (`ubuntu-26.04-desktop-amd64.iso`)
* **Allocated RAM:** 4000 MB (4 GB)
* **Allocated Processors:** 2 CPU Cores
* **Virtual Disk Size:** 20.00 GB (VDI Format)

---

## ⚙️ Step-by-Step Installation Process

### Step 1: Create a New Virtual Machine
1. Launch **Oracle VM VirtualBox Manager**.
2. Click on the **New** (+) button to start the Virtual Machine creation wizard.
3. Configure basic settings:
   * **Name:** `OS`
   * **Folder:** `C:\Users\CC\VirtualBox VMs`
   * **Type:** Linux
   * **Version:** Ubuntu (64-bit) / Debian

---

### Step 2: Configure Virtual Hardware Allocation
1. **Base Memory (RAM):** Set memory allocation to **4000 MB** (4 GB).
2. **Processors:** Assign **2 CPUs** to ensure smooth execution.
3. Check options as needed and proceed by clicking **Next**.

---

### Step 3: Virtual Hard Disk Setup
1. Select **Create a Virtual Hard Disk Now**.
2. Set the Virtual Hard Disk file size to **20.00 GB**.
3. Choose file type format as **VDI (VirtualBox Disk Image)**.
4. Click **Finish** to initialize the virtual machine container.

---

### Step 4: Attach Ubuntu ISO Image to Storage
1. Select the created VM (`OS`) and click **Settings**.
2. Navigate to the **Storage** section on the left sidebar.
3. Under **Storage Devices**, select the empty optical drive (`Controller: IDE`).
4. Attach the ISO image file: `ubuntu-26.04-desktop-amd64.iso`.
5. Click **OK** to save the settings.

---

### Step 5: Booting and Desktop Initialization
1. Select the VM and click **Start** (Green arrow icon).
2. The virtual machine boots into the live environment.
3. Once booted, the **Ubuntu Desktop** environment appears with the **Install Ubuntu** shortcut icon on the desktop.

---

## 📊 Configuration Summary

| Property | Value / Allocation |
| :--- | :--- |
| **Virtual Machine Name** | OS |
| **Base RAM Memory** | 4000 MB (4 GB) |
| **CPU Cores** | 2 Processors |
| **Storage Allocation** | 20.00 GB (VDI Format) |
| **ISO File Attached** | `ubuntu-26.04-desktop-amd64.iso` |
| **Installation Status** | Successfully Booted to Desktop |

---

## 🏁 Conclusion

The setup and configuration of the Ubuntu Linux virtual machine in Oracle VM VirtualBox were completed successfully. The guest OS is now ready for performing operating system laboratory practicals and terminal utilities.

