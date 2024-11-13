---
title: "My Homelab Setup: Proxmox, Networking, and More"
date: 2024-03-20
categories: [homelab, infrastructure]
tags: [proxmox, networking, servers, truenas]
---

# My Homelab Setup

Here's my detailed homelab setup including my experiences with Proxmox, networking, and more...

# Setting Up TrueNAS Scale: A Comprehensive Guide for Beginners

Are you looking to create a powerful and flexible Network Attached Storage (NAS) solution for your homelab? Look no further than TrueNAS Scale! In this beginner-friendly guide, i'll walk you through the process of setting up TrueNAS Scale on a virtual machine (VM) using Proxmox, configuring storage pools, creating datasets, and setting up SMB shares for secure access to your data.

## Learning Objectives
- Install TrueNAS Scale on a Proxmox VM
- Pass through physical hard drives to the TrueNAS VM
- Create storage pools and datasets
- Configure SMB shares with access control lists (ACLs)
- Mount the SMB share on your local machine

## Prerequisites
- A Proxmox server with sufficient resources (32 GB RAM, 4 CPU cores, 32 GB storage)
- Physical hard drives to pass through to the TrueNAS VM
- A network connection to access the TrueNAS web interface

## Step 1: Create a TrueNAS Scale VM in Proxmox
1. In the Proxmox web interface, create a new VM with the following specs:
   - RAM: 32 GB
   - CPU Cores: 4
   - Storage: 32 GB (for the TrueNAS installation)
2. During the installation, set a secure password and allow EFI boot.
3. Complete the installation and reboot the VM.

## Step 2: Access the TrueNAS Web Interface
1. After the reboot, note down the IP address displayed on the VM console.
2. Open a web browser and enter the IP address to access the TrueNAS web interface.
3. Log in using the default username "admin" and the password you set during installation.

## Step 3: Create a New User Account
1. In the TrueNAS web interface, go to "Credentials" > "Local Users".
2. Click "Add" to create a new user account with your desired username and password.
3. Set the user's primary group to "admin" and select the "zsh" shell.
4. Save the new user account and log out of the web interface.
5. Log back in using your new user account credentials.

## Step 4: Pass Through Physical Hard Drives to the TrueNAS VM
1. Shut down the TrueNAS VM in Proxmox.
2. SSH into your Proxmox server using a terminal.
3. Install the "lshw" (list hardware) package by running `apt install lshw`.
4. Run `lshw -class disk -class storage` to list the available hard drives and their serial numbers.
5. Note down the serial numbers of the drives you want to pass through to the TrueNAS VM.
6. For each drive, run the following command, replacing `<VM_ID>`, `<SCSI_ID>`, and `<DRIVE_ID>` with the appropriate values:
   ```bash
   qm set <VM_ID> -scsi<SCSI_ID> /dev/disk/by-id/<DRIVE_ID>
   ```
   Example:
   ```bash
   qm set 100 -scsi1 /dev/disk/by-id/ata-WDC_WD20EFRX-68EUZN0_WD-WCC4M1KPCK53
   ```
7. Start the TrueNAS VM.

## Step 5: Create a Storage Pool and Dataset
1. In the TrueNAS web interface, go to "Storage" > "Pools" and click "Add".
2. Enter a name for your pool (e.g., "big_boy") and click "Create Pool".
3. Select the disks you want to include in the pool and choose a layout (e.g., mirror).
4. Click "Save" and then "Create Pool" to create the storage pool.
5. After the pool is created, click "Add Dataset".
6. Enter a name for your dataset (e.g., "nas_share") and select "SMB" as the share type.
7. Set the SMB share name (e.g., "big_boy") and click "Save".

## Step 6: Configure SMB Share and Access Control List (ACL)
1. Go to "Sharing" > "SMB Shares" and click on the share you just created.
2. Click on the shield icon to edit the ACL settings.
3. Set the owner and owner group to your user account.
4. Remove the "builtin_users" and "builtin_administrators" from the ACL.
5. Apply the permissions recursively and click "Save Access Control List".

## Step 7: Mount the SMB Share on Your Local Machine
1. On a Mac, open Finder and click on "Network".
2. Look for your TrueNAS server and click on it.
3. If prompted, enter your user account credentials.
4. Double-click on the SMB share to mount it and start accessing your files.

Congratulations! You have successfully set up TrueNAS Scale on a Proxmox VM, passed through physical hard drives, created a storage pool and dataset, configured an SMB share with ACLs, and mounted the share on your local machine. This project has provided you with valuable skills in storage management, virtualization, and network file sharing. Feel free to explore more advanced features of TrueNAS Scale, such as snapshots, replication, and plugins, to further enhance your NAS setup.