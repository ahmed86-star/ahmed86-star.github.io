---
layout: post
title: "Wazuh SIEM Setup on Debian 12 with Proxmox"
date: 2024-03-20
categories: [cloud, security]
tags: [wazuh, siem, debian, proxmox]
---

---
date: 2024-11-05
---


# Wazuh-SIEM-Setup-Debian12-Proxmox   



![image](https://github.com/user-attachments/assets/d586c690-25af-434e-ac20-f7fdb5993659)




## **Setting up the virtual machine on proxmox**

![Screenshot 2024-11-01 204234](https://github.com/user-attachments/assets/7117abca-5a7d-4295-8fad-b2367bc0a71e)

Give it a name and choose "Next"; next, in the box that pops up, choose an OS to run on the wazuh machine; we use Debian 11/12.

![Screenshot 2024-11-01 204330](https://github.com/user-attachments/assets/b04417b8-805f-4b3e-b26d-9b050d3ade1a)

Just tick the box for Qemu Agent in the System pane; everything else should be left alone.

![Screenshot 2024-11-01 204403](https://github.com/user-attachments/assets/725d53f9-ba00-4ff7-be30-226475e1f098)


Determining the power requirements of our SIEM server is the next step. Although we will make a small adjustment, the following figures are recommended by the documentation.

![image](https://github.com/user-attachments/assets/aa39ba26-0e06-47e6-9f68-96ac8e2733f8)



In the disk configuration, provide sufficient disk space for the VM; Wazuh suggests around 50GB for every 90 days of storage, given that my SIEM does not operate continuously. I selected a total disk space of 50GB.

![Screenshot 2024-11-01 204603](https://github.com/user-attachments/assets/883c8440-e4a7-46b3-ab13-b90ea3f51e51)

The quantity of CPU cores (4) was derived from the guidelines in the Wazuh datasheet. This is sufficient; you may also manage with three.

![Screenshot 2024-11-01 204641](https://github.com/user-attachments/assets/4d37b074-1312-4662-aeea-b7d6d2c730a9)

I have been use 4GB (4096 MB) of RAM, which operates efficiently with 4-8 agents reporting to the SIEM. If you own additional memory, you may enhance this to 8GB (8192 MB).

![Screenshot 2024-11-01 204716](https://github.com/user-attachments/assets/e58f0b84-29be-4167-8130-79ce3b5633c2)


For a network device, we utilize the traditional VirtIO (paravirtualized) if an additional network bridge has been deployed outside of vmbr0.

![Screenshot 2024-11-01 204818](https://github.com/user-attachments/assets/83e28980-b2ca-4baf-a093-fa5a53d64c62)

Next up we confirm all the settings and press the ```finish``` button.

![Screenshot 2024-11-01 204853](https://github.com/user-attachments/assets/5c8affb0-f26c-49e0-a036-5e4a0dddfdfb)


***Installing Debian on the virtual machine***

Upon initiating the virtual computer, the installation of the operating system starts automatically.

I recommend the graphical installation option for aesthetic appeal.

![Screenshot 2024-11-01 205039](https://github.com/user-attachments/assets/a4a7babf-d99b-419b-875a-a63bb9bbed4a)

The initial step is picking a language; choose your preferred option, and we will proceed with standard English.

![Screenshot 2024-11-04 221301](https://github.com/user-attachments/assets/ce0ef56e-84ec-407c-a706-d78a7fe70901)

Next up is the location selection - this will be used later on for time zones as well so make sure to select the correct one for you and press the continue button.

![Screenshot 2024-11-04 221349](https://github.com/user-attachments/assets/d3348404-7e70-4dc3-9364-218f59ee4533)

Now you need to choose the correct keyboard layout and hop on to the next selection screen.

![Screenshot 2024-11-04 221429](https://github.com/user-attachments/assets/34953188-726d-42dc-977b-a46ee0310799)

## **User configured Debian**

It is time to choose a name to your machine; select something meaningful or adhere to your existing naming convention.

![Screenshot 2024-11-04 221606](https://github.com/user-attachments/assets/eed375f8-03e2-4474-8188-3849e13e76fe)


If your SIEM is to be integrated into an Active Directory Domain, you may input the domain name now; otherwise, you may configure it later if you are uncertain at this moment.

![Screenshot 2024-11-04 221711](https://github.com/user-attachments/assets/45ad945a-7795-433c-8a25-4c64e6d09c86)

Debian will configure a minimum of two users for you: one root user (administrator) and one standard user.

Initially, input the password for the root (system administrative) user twice; upon completion, you may provide a name to your standard user.

![Screenshot 2024-11-04 221743](https://github.com/user-attachments/assets/046df92a-46ed-44b6-9efa-c73cef8cf71c)

This user is the one you would use to log in for daily operations. Ensure that you remember this identity or add a notation to the VM.

![Screenshot 2024-11-04 221835](https://github.com/user-attachments/assets/a4912f29-36e1-459f-b83a-344984c20bc8)

Once the username is selected you enter a password for this user twice and continue onwards.

![Screenshot 2024-11-04 221743](https://github.com/user-attachments/assets/e12ef921-3857-4680-adf7-4dc9084000b3)

I previously mentioned that the time zone selection is restricted by the country you select. Now, comes the time zone selection. Ideally, you have chosen the correct option and are able to locate your time zone at this time. If not, you may either select a random time zone and modify it at a later time or return to the country selection section.

![Screenshot 2024-11-04 221937](https://github.com/user-attachments/assets/56967e42-f012-4691-b82e-4f5c65a94ec4)

## **Debian disk configuration**

Next, you have the option of selecting either a guided or manual approach to configuring the disk for your Debian installation. I recommend that you select the first option, ```Guided - use entire disk``` .

![image](https://github.com/user-attachments/assets/40c27021-a643-431f-b2a6-c3da142492cd)

Three more steps of single-select-and-continue workflows are coming up. The first step is to choose a disk; assuming you've been following along so far, you should only have one disk accessible. Pick that option and go on.

![Screenshot 2024-11-04 222022](https://github.com/user-attachments/assets/ebe573cf-7718-4976-8227-177d2a02f1fd)


A single partition (or several "virtual hard drives") or several ones are now an option; for simplicity's sake, I recommend utilizing the former.

![Screenshot 2024-11-04 222049](https://github.com/user-attachments/assets/8cbbbf24-d147-46aa-be8d-d7c1238603a6)


At this point, you should confirm the partitioning and disk erasure as all the specifics have been worked out.


Confirm once more and you are done with the disk setup.

![Screenshot 2024-11-04 222125](https://github.com/user-attachments/assets/239a4e6d-4c26-4473-ad95-742d08ac6909)

## **Debian software installation**

To ensure that your Debian remains current, you will require software updates. The initial selection interface will provide you with the option to install packages/libraries from an external hard drive or USB disk. Given that you are unlikely to possess one, you may select ```No``` and proceed.

![Screenshot 2024-11-04 222504](https://github.com/user-attachments/assets/39cfbe73-a9c3-4bf3-b3d5-ab838cebcf8f)

debian uses ```apt``` (Advanced Package Tool) for most of the software installation. Apt works with mirrors + archives which hold the actual libraries you want to install and since the world is a big place you can choose the mirror location closest to you to have minimum latency.

You can leave this in the default setting, it should not have much impact on your daily work.

![Screenshot 2024-11-04 222543](https://github.com/user-attachments/assets/700eb202-0e24-4ee7-a87c-d0a13b6f2c07)


The mirror selection process is now underway; simply leave it at ```deb.debian.org``` and proceed.

![Screenshot 2024-11-04 222615](https://github.com/user-attachments/assets/54d57338-d914-462f-ad6d-5594959492e3)

If your internet is proxied, you may now input the appropriate proxy information. If you have not yet established a proxy, it is likely a wise decision to leave this field vacant.

![Screenshot 2024-11-04 222646](https://github.com/user-attachments/assets/c35073fb-873e-45d9-8675-cb0a48b758e5)

Now, the option to share anonymous usage data for the packages you installed/use is presented. I select "No" due to my aversion to telemetry data collection, regardless of whether it is anonymous.

![Screenshot 2024-11-04 223003](https://github.com/user-attachments/assets/b62a5a52-bd24-46da-a873-a25624d59483)

If you're new to this, you might be confused about the following step, but don't worry; it's not hard.

The default configuration includes the Debian desktop environment, GNOME, and basic system tools, but you may change it if you choose. Debian, KDE Plasma, and the standard system utilities are my preferred desktop environments because I prefer KDE (a bottom-mounted taskbar comparable to Windows or Mac) to gnome.

It is possible to connect to the virtual machine (VM) without the desktop environment, but you will likely require an SSH server for this.

![Screenshot 2024-11-04 223053](https://github.com/user-attachments/assets/b406f59f-a8d3-486f-be8b-cea00fae8d4d)


## **Installing Debian is now complete.**

Selecting "yes" in response to the next question will enable you to configure the grub boot loader, the last stage.


![image](https://github.com/user-attachments/assets/57d88cc1-da8a-499a-8092-be22edc884ed)





The final stage in installing Debian is to install the boot loader on the one and only disk we have.

![image](https://github.com/user-attachments/assets/8e4d0398-51fe-4c55-b96c-e768bd3bb839)

![image](https://github.com/user-attachments/assets/ac8aa62c-1c49-488e-a32d-e3f8c0074e88)


Start again and log in using the account you created before.


Wazuh SIEM installation
A visit to https://documentation.wazuh.com/current/quickstart.html#installing-wazuh is required, followed by copying the displayed command.

![Screenshot 2024-11-05 022117](https://github.com/user-attachments/assets/73dc2b5a-bd89-40b7-a638-e14fdd1d6c91)


Curl is not installed by default on Debian, therefore we need to install it before the installation can begin.

To begin, just copy and paste the commands provided below.


# first we become root so that we can install packages

```su ```
```# next install curl```
```apt-get install curl```
```# and install wazuh```
```curl -sO https://packages.wazuh.com/4.9/wazuh-install.sh && sudo bash ./wazuh-install.sh -a```

![Screenshot 2024-11-04 230646](https://github.com/user-attachments/assets/3917f6fd-9b47-46ee-ab33-e07604a240ff)

![Screenshot 2024-11-04 230928](https://github.com/user-attachments/assets/a4afb240-356b-4fe1-8f5b-3b78594ce19e)

![Screenshot 2024-11-04 231219](https://github.com/user-attachments/assets/05876831-1940-4cd5-9e6c-102ced3d24ca)


Make sure to copy and paste the username/password combination into your password manager at the end.

![Screenshot 2024-11-05 023213](https://github.com/user-attachments/assets/3ce62405-436f-49bb-b836-1416f8f9b970)


Wazuh should now be operating on your computer if the installation was successful.

Tell me how to get to it!

Thanks for asking! To access the SIEM machine, either open the browser on that device or, if you want to connect remotely, use https://<IP_of_your_wazuh_machine>.

Because it does not originate from a certificate authority (CA), you can expect to get an error message stating that the Server's certificate is not trusted.

You will be welcomed by the Wazuh login page, therefore you may safely disregard this mistake.

![image](https://github.com/user-attachments/assets/1022e597-d375-438e-ac1b-d5341b91c942)

![Screenshot 2024-11-05 010559](https://github.com/user-attachments/assets/a21bfc9c-14bc-4474-9c69-9415035db39d)


Upon logging in, Wazuh will verify that its APIs and services are available. Once that is complete, the dashboard will be shown.

![Screenshot 2024-11-05 010716](https://github.com/user-attachments/assets/ac836804-5853-4fa8-ab43-8f1ea7ae5171)


The dashboard looks like this and while yours will not have any agents registered you can do that next.

![image](https://github.com/user-attachments/assets/0329a0a0-2e0e-4c5e-a3b3-3c7306fcd242)