---
layout: post
title: "Azure Wireshark Network Lab: Hands-on Network Analysis"
date: 2024-03-20
categories: [cloud, networking]
tags: [azure, wireshark, network-analysis, lab]
---

# Azure Wireshark Network Lab

# Azure-Wireshark-Network-Lab
A lab to observe network traffic protocols to and from Azure VMs using Wireshark and experiment with Network Security Groups
![image](https://github.com/ahmed86-star/Azure-Wireshark-Network-Lab/assets/113064932/ad6a0d2c-3847-45fa-850d-3e994f63f60d)

## Environments and Technologies Used
- Microsoft Azure (Virtual Machines: Windows 10 Pro, Ubuntu, and Windows 11)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

## Lab Setup
## References
- [Wireshark Documentation](https://www.wireshark.org/docs/)
- [Microsoft Azure Documentation](https://docs.microsoft.com/en-us/azure/)
  
### Step 1: Set Up Azure Virtual Machines
1. **Create Virtual Machines**:
    - Windows 10 Pro
    - Ubuntu
    - Windows 11
2. **Configure Network Settings**:
    - Assign static IPs if necessary
    - Set up Network Security Groups (NSGs)

### Step 2: Install Necessary Tools
1. **On Windows VMs**:
    - Install Wireshark
    - necessary command-line tools (e.g., PowerShell, Command Prompt)
2. **On Ubuntu VMs**:
    -ping ip

   ### Step 3: Configure Remote Desktop
- Ensure Remote Desktop is enabled on all Windows VMs.
  ![image](https://github.com/ahmed86-star/Azure-Wireshark-Network-Lab/assets/113064932/37a7b041-1497-407a-85db-7490ceed5e87)
- Set up SSH access for Ubuntu VM.
  
### Step 4: Experiment with Network Traffic
1. **Capture Network Traffic with Wireshark**:
   ![image](https://github.com/ahmed86-star/Azure-Wireshark-Network-Lab/assets/113064932/dff18278-38f0-4817-a638-39b58a44948a)
   
    - Start capturing traffic on each VM.
    - Generate traffic using various protocols (SSH, RDH, DNS, HTTP/S, ICMP).
      ![image](https://github.com/ahmed86-star/Azure-Wireshark-Network-Lab/assets/113064932/31d1f2c2-6b3c-47cb-b060-af83a2333f59)

      2. **Analyze Traffic**:
    - Observe and analyze the captured traffic.
      ![image](https://github.com/ahmed86-star/Azure-Wireshark-Network-Lab/assets/113064932/f8119c6f-1902-4439-ae27-b25a2caaa63d)
    - Document your findings
![image](https://github.com/ahmed86-star/Azure-Wireshark-Network-Lab/assets/113064932/c96b6fe4-92ba-416d-922c-629d1a8eca78)

### Step 5: Experiment with Network Security Groups
1. **Configure NSGs**:
   ![image](https://github.com/ahmed86-star/Azure-Wireshark-Network-Lab/assets/113064932/e989eaec-8702-4648-9d45-e6ac7427d137)
    - Set up rules to allow or deny specific traffic.
      ![image](https://github.com/ahmed86-star/Azure-Wireshark-Network-Lab/assets/113064932/15f4ad35-017c-473c-b4f4-91d0897b9dcb)

3. **Test Traffic**:
    - Test connectivity with different NSG rules.


Summary

 This lab successfully met its objectives of observing network traffic and experimenting with security configurations. The hands-on experience I gained through this project is invaluable for deepening my understanding of network protocols and cybersecurity measures in a cloud environment. By documenting the process and findings, this lab also serves as a useful reference for future projects and learning.

Overall, this lab project underscores the critical role of network traffic analysis and security configurations in maintaining secure and efficient cloud-based environments.
      


   