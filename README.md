## Cybersecurity Lab Setup: Kali Linux on VirtualBox

## Week 1 Project CyberSecurity Internship (Networkwalks,Batch B084C)


## About This Project
This is my Week 1 project from the CyberSecurity Internship at Networkwalks. The task was to build a safe practice lab on my own computer where I can learn ethical hacking without touching any real system.
I installed Oracle VirtualBox,created a private NAT Network,imported Kali Linux,set up a static IP address and saved a snapshot as a backup.Everything is written step by step so any beginner can follow along.

## What You Need

| Item | Details |
|---|---|
| Computer | Windows laptop or PC |
| RAM | At least 8 GB (I gave Kali 4GB) |
| Free disk space | About 25 GB |
| Software | Oracle VirtualBox 7.2.12, Kali Linux 2026.2 (VirtualBox image), 7-Zip |
| Internet | Needed to download the files |

## My Lab Settings

| Setting | Value |
|---|---|
| Hypervisor | Oracle VirtualBox 7.2.12 |
| Guest OS | Kali Linux 2026.2 (amd64) |
| Network type | NAT Network, named NatNetwork |
| Network range | 10.0.0.0/24 (DHCP on) |
| Kali IP address | 10.0.0.2 |
| Netmask | 24 |
| Gateway | 10.0.0.1 |
| DNS | 8.8.8.8 |
| Adapter | Intel PRO/1000 MT Desktop |
| Promiscuous mode | Allow All |

---

## Step 1: Download VirtualBox and Kali Linux

1. Go to the official VirtualBox website and download the installer for Windows.(https://www.virtualbox.org/wiki/Downloads)
2. Go to the official Kali Linux website, open the "Virtual Machines" section and download the VirtualBox image (64-bit).(https://www.kali.org/get-kali/#kali-virtual-machines)
3. Download 7-Zip, because the Kali file comes as a .7z archive.(https://www.7-zip.org/)


## Step 2: Install VirtualBox

1. Double click the VirtualBox installer.
2. Click Next and keep the default options.
3. Click Install and wait for it to finish.
4. Open VirtualBox Manager to make sure it starts properly.


## Step 3: Add a NAT Network

A NAT Network lets the virtual machines talk to each other and use the internet, while staying hidden from the rest of my home network. This keeps the lab safe.

1. In VirtualBox, go to *File > Tools > Network*.
2. Open the *NAT Networks* tab and click *Create*.
3. Set the name to NatNetwork.
4. Set the IPv4 Prefix to 10.0.0.0/24.
5. Keep *Enable DHCP* ticked.
6. Click *Apply*.


## Step 4: Import Kali Linux into VirtualBox

1. Right click the Kali .7z file and extract it with 7Zip.
2. Open the extracted folder and doubleclick the .vbox file. Kali will appear in VirtualBox.
3. Select Kali and click *Settings > Network*.
4. For Adapter 1, change *Attached to* from NAT to NAT Network and choose NatNetwork.
5. Set *Promiscuous Mode* to Allow All. This helps later when capturing network traffic.
6. Click *OK*.

I also checked the System tab (boot order and acceleration) and the Shared Folders tab, to make sure everything looked correct.


## Step 5: Configure IP Settings Inside Kali Linux

Start the Kali VM and log in (default username kali, password kali). Please change the password later.

1. Open *Advanced Network Configuration* and edit *Wired connection 1*.
2. Go to the *IPv4 Settings* tab and change the method to *Manual*.
3. Click *Add* and enter:
   - Address: 10.0.0.2
   - Netmask: 24
   - Gateway: 10.0.0.1
4. In the DNS servers box, type 8.8.8.8.
5. Click *Save*.


Now open the terminal and restart the connection so the new settings apply:

bash

sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0

sudo nmcli connection down "Wired connection 1"

sudo nmcli connection up "Wired connection 1"


The first command removes a small waiting delay when the connection starts. The next two turn the connection off and on again.


### Check the Internet

Run these commands to confirm everything works:

bash

ip a

ping -c 4 10.0.0.1

ping -c 4 8.8.8.8

ping -c 4 google.com


I also opened Firefox inside Kali and searched on Google. The page loaded, so the internet is working.


## Step 6: Take a Snapshot Backup

A snapshot saves the exact state of the VM. If I break something later, I can go back in a few clicks.

1. Shut down the Kali VM.
2. In VirtualBox, select Kali and open the *Snapshots* tab.
3. Click *Take*.
4. Name: My first Kali Linux setup
5. Description: Internet connection is working fine
6. Click *OK*.


## Problems I Faced and Fixes

| Problem | Fix |
|---|---|
| No internet in Kali | Check that Adapter 1 is set to NAT Network and that the IP, gateway and DNS are correct |
| New IP not working | Run the nmcli down and up commands again, or restart the VM |
| Network takes long to connect | Set ipv4.dad-timeout to 0 |
| VM does not start | Turn on virtualization (VTx/AMD-V) in the BIOS |

## What I Learned

- How to install and use VirtualBox
- The difference between NAT and NAT Network
- How to set a static IP address in Linux
- How to use nmcli to manage connections
- Why snapshots are important before testing anything

## Next Steps

- Add a vulnerable machine to practice on
- Set up Wazuh for security monitoring
- Practice scanning with Nmap and traffic analysis with Wireshark

## Disclaimer

This lab is only for learning. I will only test systems that I own or have permission to test.

## Acknowledgement

Thank you to *Networkwalks*  and my instructors for the guidance in this internship.

## Author

*Tabia Babar*

Cybersecurity Intern,Networkwalks(Batch B084C)

LinkedIn: www.linkedin.com/in/tabia-babar

GitHub: https://github.com/Tabia-Babar

