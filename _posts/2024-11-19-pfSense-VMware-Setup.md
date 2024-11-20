---
title: "pfSense VMware Setup"
date: 2024-11-19
categories: [Networking, Virtualization]
tags: [pfSense, VMware, Setup]
---



![Screenshot 2024-11-19 144846](https://github.com/user-attachments/assets/aaf352fe-b7a4-4afd-9d80-d9d24dd21632)

# pfSense-VMware-Setup
A step-by-step guide to installing and configuring pfSense 2.7.2 on VMware.

## pfSense 2.7.2 on VMware
This repository contains a detailed guide on installing and configuring pfSense 2.7.2 on VMware Workstation/ESXi for a robust firewall solution.

## Prerequisites
- VMware Workstation/ESXi
- pfSense 2.7.2 ISO
- 2GB RAM, 20GB disk (minimum for pfSense)
- Basic knowledge of networking

## Key Features
- Setting up NAT and firewall rules
- Configuring DHCP and DNS services
- Enabling VPN functionality

### 1. Overview of pfSense 2.7.2
Because of its adaptability, pfSense, an open-source firewall and router platform based on FreeBSD, is often used in both home and business networks. This tutorial will cover the first setup stages and show you how to install pfSense 2.7.2 on a VMware virtual machine.

### 2. Downloading pfSense 2.7.2
First, download the pfSense installer from the official pfSense website: [pfSense Download](https://www.pfsense.org/download/)

- **Architecture**: Select “AMD64” for modern 64-bit systems.
- **Installer Type**: Choose the “ISO Installer” for use with VMware.
- **Mirror**: Select a mirror close to your location for faster download.

Once downloaded, you can use this ISO to create a virtual machine in VMware.

### 3. Installation Process in VMware
After downloading the ISO file, follow these steps to set up a virtual machine in VMware:

#### 1. Create a New Virtual Machine:
Open VMware and click Create a New Virtual Machine. Choose Typical configuration for simplicity. Select the Installer disc image file (ISO) option, and browse to the downloaded pfSense ISO.

#### 2. VMware Configuration:
Name the virtual machine (e.g., pfSense_VM).

#### 3. Network Layout:
Put two network adapters in the VMware configurations. One for the WAN interface—set "Bridged" or "NAT," depending on your network. One for the LAN interface, designated "Host-only" to keep it apart from the outside network.

![Screenshot 2024-11-18 235447](https://github.com/user-attachments/assets/5c43099a-a07d-4639-9c6b-5fc7bde82304)

#### 4. Start the virtual machine then install pfSense:
You will get the pfSense installation when booting the VM. Out of the menu, choose "Install pfSense". Unless you want a special setup, select the Auto (ZFS) for disk partitioning.

![Screenshot 2024-11-18 235810](https://github.com/user-attachments/assets/1b9fcf66-86df-4205-826f-7717bacbb29e)

Click enter to proceed to install pfSense.

![Screenshot 2024-11-18 235905](https://github.com/user-attachments/assets/c4098b8b-4ca8-4257-89df-5310860492d6)

Indeed, Auto (ZFS) for disk partitioning is fine unless you want a customized setup.

![Screenshot 2024-11-19 000251](https://github.com/user-attachments/assets/77d74827-2e5c-44ce-8ea7-743efdc0d2bf)

![Screenshot 2024-11-19 000330](https://github.com/user-attachments/assets/5d9756b6-fa94-42e0-a527-d953de895fd9)

![Screenshot 2024-11-19 000403](https://github.com/user-attachments/assets/2ff668e5-abe3-4bcc-adde-ed951a3d9649)

![Screenshot 2024-11-19 000447](https://github.com/user-attachments/assets/1d479d66-fe09-4b9c-8568-ec4816aacfbf)

![image](https://github.com/user-attachments/assets/2dfc164c-274f-4bd0-958c-7b80695da7af)

### 5. Reboot the VM:
After installation, the VM will reboot, and pfSense will start for the first time.

![Screenshot 2024-11-19 002026](https://github.com/user-attachments/assets/ebe4fc66-f25b-41cd-914b-af92e0347e28)

![image](https://github.com/user-attachments/assets/6a5f0150-7703-4551-b8bc-f68db802b371)

### Basic Configuration:
Once pfSense has successfully booted and is running, you need to log in to the web interface to perform the initial setup.

1. **Access the Web Interface**: Open a web browser and navigate to `http://192.168.4.20` (or the LAN IP address you configured).
2. **Login with Default Credentials**: Use the default login credentials:
   ```plaintext
   Username: admin
   ```

![Screenshot 2024-11-19 010558](https://github.com/user-attachments/assets/1d6db33c-dfa5-43a8-a7ff-d02975e171cb)

### Change the Admin Password:
After logging in, pfSense will prompt you to change the default admin password. Make sure to set a strong, secure password to protect your firewall.

![image](https://github.com/user-attachments/assets/a1242b1e-470e-48dc-bbd6-d437631eb7ec)

![image](https://github.com/user-attachments/assets/eb14b018-83da-4b24-9d71-29c490fa1155)

### Configure Domain and Hostname:
Subsequent to altering the administrator password, it is necessary to modify the domain and hostname.

- Browse to **System > General Setup**.
- Enter the desired hostname (e.g., pfSense) in the Hostname field.
- Enter the domain (e.g., localdomain or your organization's domain) in the Domain field.
- To implement the modifications, navigate to the bottom of the page and select "Save."

### Configure DNS Servers:
If you possess a local DNS server, you may configure it in pfSense:

- Scroll down to the DNS Server Settings section in **System > General Setup**.
- In the DNS Server field, specify the IP address of your local DNS server.
- Additionally, you may establish additional DNS servers as backup options, such as Cloudflare's `1.1.1.1` or Google's `8.8.8.8`, at your discretion.
- To implement the DNS configuration, select "Save."

![image](https://github.com/user-attachments/assets/918cf441-53ac-4205-b2a3-f7f1cc48ea4b)

### System Updates:
Keeping pfSense up to date is crucial for security and performance. Here’s how to check for updates:

- Go to **Status > Dashboard** on the pfSense web interface after logging in.
- **Check Updates**: Find the “System Information” widget on the dashboard to see the current pfSense version. If you get an update notification, continue.

To upgrade pfSense, navigate to **System > Upgrade**. Here, you can:
- **Check Updates**: Click the “Check for Updates” button to check for new updates.
- Choose an update and follow the steps to apply it. Always back up your settings before updating.

**Reboot If Needed**: Updates may need rebooting. Restart pfSense to finish updating if requested.

**Verify Update Success**: Restart and check **Status > Dashboard** for the latest update. Version shown is current.

![image](https://github.com/user-attachments/assets/1e4ad2bf-9723-4a6d-b577-82183dd76fdd)

Feel free to contact me for help if you run into any problems with the setup, configuration, or update procedures.
