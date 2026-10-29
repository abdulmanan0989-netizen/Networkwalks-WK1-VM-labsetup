Week 01 - Cybersecurity Lab Setup
* *01* = Step 4: Kali VM Import & Running
* *02* = Step 4: Kali Desktop
* *03* = Step 5: Manual IP Configuration `10.0.0.2`
* *04* = Step 3: NAT Network `10.0.0.0/24` Creation
* *05* = Step 2: VirtualBox Welcome
- *06* = Step 6: Clean Snapshot
 Copy this full README for GitHub:
🔐 Cybersecurity Lab Environment Setup
Building an isolated virtual lab for penetration testing and ethical hacking practice

📌 Project Overview
This project focuses on setting up a virtual cybersecurity and penetration-testing laboratory using **VirtualBox** and **Kali Linux**.

The purpose of the lab is to create a controlled environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly.

The lab is configured on a private virtual network so that additional machines can be added later and used as targets for authorized security testing.

🎯 Objectives
- Install and configure VirtualBox.
- Install/import Kali Linux as a virtual machine.
- Create a private NAT Network for the cybersecurity lab.
- Configure network connectivity for Kali Linux.
- Assign a consistent IP address to the Kali VM.
- Verify network connectivity and DNS resolution.
- Take a clean VM snapshot for recovery.
- Document the complete setup process.
- Prepare the environment for future cybersecurity projects.

🛡️ Purpose of the Lab
The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing.

It can be used for activities such as:
- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice
- Security-tool experimentation

 🏗️ Lab Architecture

[ Host OS: Windows 10 ]
      |
      +-- [ VirtualBox 7.2 ]
            |
            +-- [ NAT Network: NatNetwork 10.0.0.0/24 ]
                  |
                  +-- [ Kali Linux 2026.3 - 10.0.0.2/24 ]
                  +-- [ Future Targets: 10.0.0.3-10.0.0.99 ]
                  |
                  +-- Gateway: 10.0.0.1 / DNS: 8.8.8.8 -> Internet

 ⚙️ Lab Configuration
| Component | Configuration |
|---|---|
| Host OS | Windows 10 |
| Host RAM | 8 GB |
| Processor | Intel Core i7 |
| Hypervisor | VirtualBox 7.2 |
| Security OS | Kali Linux 2026.3 |
| Kali RAM | 2048 MB |
| Virtual Network | NAT Network - NatNetwork |
| Network Address | 10.0.0.0/24 |
| Kali IP Address | 10.0.0.2/24 |
| Gateway | 10.0.0.1 |
| DNS Server | 8.8.8.8 |
| Future VM Range | 10.0.0.3–10.0.0.99 |

🪜 Lab Setup Procedure

Step 1. Install 7-Zip
7-Zip was installed to extract the Kali Linux VM package (.7z archive).

Step 2. Install VirtualBox
VirtualBox was installed as the hypervisor.

![VirtualBox Welcome](screenshots/05-vbox-welcome.png)

Step 3. Create the NAT Network
A dedicated NAT Network was created in VirtualBox.
**Configuration:** Name: NatNetwork, IPv4 Prefix: 10.0.0.0/24, DHCP: Enabled, IPv6: Disabled

![NAT Network](screenshots/04-nat-network.png)

A NAT Network was selected because multiple VMs on same NAT Network can communicate while also having outbound connectivity.

 Step 4. Import Kali Linux
Kali Linux VM was downloaded from official site and imported. Adapter 1 -> Attached to: NAT Network, Network: NatNetwork, Type: Intel PRO/1000 MT Desktop. RAM: 2048 MB. Shared folder configured for host-guest file transfer.

![Kali Running](screenshots/01-vbox-running.png)
![Kali Desktop](screenshots/02-kali-desktop.png)

Step 5. Configure the Kali Linux Network
Consistent IPv4 configured:
IP: 10.0.0.2, Netmask: 24, Gateway: 10.0.0.1, DNS: 8.8.8.8

![IP Configuration](screenshots/03-ip-config.png)

Step 6. Create a Clean VM Snapshot
After configuration, a snapshot was created.
**Snapshot Name:** kali setup / Clean Kali - Network Setup
**Description:** complete kali setup and network configuration.

![Snapshot](screenshots/06-snapshot.png)

If future exercise damages VM, it can be restored to baseline.

🔎 Lab Verification
| Test | Command | Expected Result |
|---|---|---|
| Check IP | `ip a` | 10.0.0.2/24 displayed |
| Test gateway | `ping 10.0.0.1` | Successful replies |
| Test Internet | `ping 8.8.8.8` | Successful replies |
| Test DNS | `nslookup networkwalks.com` | Domain resolves |
| Verify Nmap | `nmap --version` | Version displayed |
| Verify snapshot | Restore snapshot + `ip a` | Baseline restored |

🐞 Problems Encountered & Solutions
**Problem 1. Internet Connectivity After Static IP**
Workaround:
```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
*Problem 2. VirtualBox VT-x / Virtualization Error*
VM failed to start - hardware virtualization disabled in BIOS. Fixed by entering BIOS/UEFI and enabling Intel VT-x, saving, restarting.
💡 What I Learned
1. *NAT vs NAT Network* - NAT Network allows VM-to-VM communication + external connectivity.
2. *Virtual Machine Networking* - How VirtualBox adapters connect VMs.
3. *Static IP Configuration* - Configuring IPv4, gateway, DNS in Kali.
4. *VM Snapshots* - Creating clean baseline before risky activities.
5. *Documentation* - Documenting commands, screenshots, problems is professional practice.

🔐 Security & Ethical Use
This laboratory is intended strictly for education purposes only.

🔗 Tools & Resources
- 7-Zip: https://7-zip.org/download.html
- VirtualBox: https://virtualbox.org/wiki/Downloads
- Kali Linux: https://kali.org/get-kali
📌 Project Information
Program Name: Cybersecurity at Networkwalks | Week: 01 | Project: Cybersecurity & Pentesting Lab Setup
