# **Home Lab Build — Part 1: Virtual Network Infrastructure & Kali Linux Setup**

**Author:** Breon Hopkins  
 **Date:** May 2026  
 **Host Platform:** Windows (Microsoft Surface Pro 3\)  
 **Virtualization Platform:** Oracle VirtualBox

## **Project Overview**

This project documents the end-to-end setup of a cybersecurity home lab environment on a Windows-based personal device. As my first hands-on cybersecurity project, this lab was designed to establish foundational skills in virtualization, network configuration, and system deployment within a controlled environment.

The objective of Part 1 was to install and configure a virtualization platform, create custom virtual networks via command-line tools, and deploy a Kali Linux virtual machine within those networks.

This lab serves as the foundation for future work in penetration testing, network analysis, and security research.

## **Objectives**

* Install Oracle VirtualBox and the Extension Pack  
* Create DHCP-enabled internal virtual networks using command-line tools  
* Deploy a Kali Linux virtual machine  
* Configure multi-network connectivity (bridged and internal)  
* Validate connectivity and apply basic system hardening

## 

## 

## 

## 

## **Tools and Technologies**

| Tool | Purpose |
| :---- | :---- |
| Oracle VirtualBox | Virtualization platform |
| VirtualBox Extension Pack | Extended VM functionality |
| Kali Linux 2026.1 (VirtualBox AMD64) | Penetration testing operating system |
| Windows Command Prompt | Network configuration via VBoxManage |
| qBittorrent | Torrent client used for OS image download |

## **Network Architecture**

Two internal virtual networks were created with DHCP enabled:

| Network Name | Gateway IP | DHCP Range | Netmask |
| ----- | ----- | ----- | ----- |
| FirstLab | 172.30.1.1 | 172.30.1.20 – 172.30.1.50 | 255.255.255.0 |
| HiddFirstLab | 10.205.1.1 | 10.205.1.20 – 10.205.1.50 | 255.255.255.0 |

### 

### **Kali Virtual Machine Network Configuration**

| Adapter | Type | Purpose |
| ----- | ----- | ----- |
| Adapter 1 | Bridged Adapter | External network and internet access |
| Adapter 2 | Internal Network (FirstLab) | Isolated lab environment |

## **Implementation**

### **Phase 1 — VirtualBox Installation**

Oracle VirtualBox was downloaded and installed on a Windows-based system. The VirtualBox Extension Pack was also installed to enable additional features such as improved hardware compatibility and extended device support.

### **Phase 2 — Virtual Network Configuration**

Using Windows Command Prompt, I navigated to the VirtualBox installation directory:

cd "C:\\Program Files\\Oracle\\VirtualBox"

Existing DHCP configurations were verified:

VBoxManage list dhcpservers

Two internal networks were then created using `VBoxManage`:

**FirstLab Network:**

VBoxManage dhcpserver add \--network=FirstLab \--server-ip=172.30.1.1 \--lower-ip=172.30.1.20 \--upper-ip=172.30.1.50 \--netmask=255.255.255.0 \--enable

**HiddenFirstLab Network:**

VBoxManage dhcpserver add \--network=HiddFirstLab \--server-ip=10.205.1.1 \--lower-ip=10.205.1.20 \--upper-ip=10.205.1.50 \--netmask=255.255.255.0 \--enable

This approach provided hands-on experience with command-line network configuration and reinforced an understanding of DHCP and subnetting concepts.

### **Phase 3 — Kali Linux Deployment**

The initial attempt to download the Kali Linux VirtualBox image via direct download resulted in repeated timeouts. To resolve this issue, I used qBittorrent to download the compressed archive.

After extraction, the following files were obtained:

* Virtual machine configuration file (.vbox)  
* Virtual disk image (.vdi), approximately 15.8 GB

During import, VirtualBox detected a UUID conflict caused by a previous failed import attempt.

**Resolution steps:**

* Removed the inaccessible virtual machine entry  
* Re-imported the virtual machine using the “Machine → Add” option

This process required troubleshooting and reinforced the importance of understanding how virtualization platforms manage machine identities.

### **Phase 4 — Virtual Machine Configuration**

Prior to booting the virtual machine, several configuration changes were made:

* Increased memory allocation to 4096 MB to improve performance  
* Configured Adapter 1 as a Bridged Adapter to enable internet access  
* Enabled Adapter 2 and connected it to the internal FirstLab network

This configuration allowed the virtual machine to operate across both an external network and an isolated lab environment.

### **Phase 5 — Kali Linux Configuration**

After successfully launching Kali Linux, system configuration and validation steps were performed.

**Network Verification:**

ip address

This confirmed that interface `eth1` received the IP address 172.30.1.20 from the FirstLab DHCP server.

**Network Adjustment:**

* Disabled IPv6 on the primary interface to simplify lab configuration and reduce unnecessary variables

**Basic System Hardening:**

passwd

* Updated the default system password to improve security

## **Results and Verification**

| Task | Status |
| :---- | ----- |
| VirtualBox and Extension Pack installed | Complete |
| FirstLab network configured | Complete |
| HiddFirstLab network configured | Complete |
| Kali Linux deployed successfully | Complete |
| DHCP IP assignment verified | Verified |
| IPv6 disabled | Complete |
| Default password updated | Complete |

## 

## **Challenges and Troubleshooting**

| Issue | Resolution |
| :---- | :---- |
| Kali Linux download failures | Switched to torrent-based download using qBittorrent |
| UUID conflict during import | Removed stale virtual machine entry and re-imported |
| Incorrect network interface showing IPv6 only | Identified correct interface (`eth1`) and validated IPv4 assignment |

## **Lessons Learned**

This project provided practical, hands-on experience in virtualization, networking, and troubleshooting. As my first cybersecurity lab, it established a strong technical foundation and highlighted several important concepts:

**Command-Line Configuration Improves Control**  
 Using `VBoxManage` demonstrated how command-line tools provide greater flexibility and precision compared to graphical interfaces, especially in repeatable or scalable environments.

**Importance of Network Validation**  
 The initial confusion between network interfaces reinforced the need to verify configurations rather than rely on assumptions. Tools such as `ip address` are essential for accurate validation.

**Troubleshooting Is a Core Technical Skill**  
 Resolving issues such as download failures and UUID conflicts emphasized the importance of systematic problem-solving and persistence when working in technical environments.

**Understanding Network Segmentation**  
 Creating multiple internal networks provided insight into how segmentation isolates traffic, a key concept in cybersecurity for both defense and testing.

**Early System Hardening Is Essential**  
 Updating default credentials and modifying network settings demonstrated the importance of securing systems immediately after deployment, even in a lab environment.

## **Repository Structure**

homelab/

├── Part1-Network-Setup/

│   ├── README.md

│   └── screenshots/

│       ├── 01-dhcp-networks-created.png

│       ├── 02-kali-vbox-error.png

│       ├── 03-network-adapter-settings.png

│       └── 04-kali-running.png

## **Conclusion**

This project represents my first hands-on cybersecurity lab and demonstrates my ability to independently design, build, and troubleshoot a virtualized network environment. All configurations were completed on personal hardware within a controlled setting.

Through this process, I developed foundational skills in virtualization, networking, and system configuration, while also strengthening my ability to diagnose and resolve technical issues. This lab serves as the starting point for continued growth in cybersecurity and hands-on technical development.

