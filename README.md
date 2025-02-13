## Introduction  
In this project, I designed and implemented a security lab to simulate real-world cyberattacks and evaluate defensive security controls. This step-by-step exercise involved configuring a vulnerable environment, launching cyberattacks, and deploying security monitoring solutions to detect and mitigate threats. The goal was to gain hands-on experience in both offensive and defensive security strategies using enterprise-grade tools.  





## Phase 1: Configuring the Security Lab  

### Network Topology and Virtual Machine Setup  
The lab environment was built using VirtualBox, simulating an enterprise network. It included the following core components:  

- **Windows Server 2025 (Active Directory Domain Controller)** – Centralized authentication and directory services.  
- **Ubuntu 22.04 Security Server** – Configured as a security monitoring station.  
- **Windows 11 Enterprise Client** – Representing an average business user machine.  
- **Ubuntu Linux Client** – Simulating a development workstation.  
- **SMTP Email Server (Postfix)** – Providing email communication for phishing simulations.  
- **Kali Linux Attacker Machine** – Used for penetration testing and cyberattack simulations.

  

![image](https://github.com/user-attachments/assets/0d1c5f23-6856-4c8f-bdf8-685d378c37ab)


### Provisioning Virtual Machines  
Each VM was provisioned with the appropriate operating system and configured according to its role in the lab. The security server was set up to monitor activities, and network configurations were designed to facilitate both attack and defense scenarios.  



## Phase 2: Creating a Vulnerable Environment  

### Introducing Security Weaknesses  
To simulate a realistic attack scenario, I intentionally misconfigured security settings on various machines, such as:  

- **Enabled SSH with root login** on Linux systems.  
- **Enabled Remote Desktop Protocol (RDP)** on Windows clients without strong authentication controls.  
- **Allowed unfiltered email communication** to facilitate phishing attacks.  
- **Stored sensitive files in predictable locations** to simulate data exfiltration risks.  

These vulnerabilities provided an ideal environment to test both offensive security techniques and defensive monitoring strategies.  



## Phase 3: Simulating a Cyberattack  

![image](https://github.com/user-attachments/assets/1effc8eb-c865-4801-882f-e57a312b3f8c)


### Reconnaissance and Initial Access  
Using **Nmap**, I conducted network scans to identify open ports and active services. I discovered that SSH and RDP were exposed, providing possible attack vectors.  

For credential-based attacks, I used **Hydra** to perform brute-force attempts on SSH, successfully gaining access due to weak passwords.  

### Phishing Attack  
To simulate a social engineering attack, I set up a **fake login page** using Apache on the attacker machine. I then crafted a phishing email using **Postfix MTA** and sent it to a target user. The victim's credentials were captured successfully when they attempted to log in.  

### Lateral Movement and Privilege Escalation  
After gaining initial access, I explored ways to move laterally across the network:  

- **WinRM Exploitation:** Used Evil-WinRM to execute commands remotely.  
- **Exploited shared credentials** to access other systems.  
- **Captured sensitive files** stored in the document folders of compromised machines.  

### Data Exfiltration  
I exfiltrated sensitive data by:  

- Using **Netcat** to transfer files between machines.  
- Establishing a **reverse shell** to maintain persistent access.  


## Phase 4: Deploying Security Monitoring with Wazuh  

### Configuring Wazuh SIEM  
To detect and respond to cyber threats, I set up **Wazuh**, an open-source SIEM solution. The following monitoring capabilities were enabled:  

- **Intrusion Detection System (IDS):** Logged brute-force SSH attempts.  
- **File Integrity Monitoring (FIM):** Tracked unauthorized file access.  
- **Log Analysis:** Monitored suspicious authentication events in Windows and Linux.  
- **Real-time Alerts:** Configured notifications for privilege escalation and failed logins.  

### Detection and Response  
With Wazuh running, I tested its detection capabilities by repeating some attack techniques. Wazuh successfully generated alerts for:  

- Multiple failed SSH logins.  
- Suspicious remote execution via WinRM.  
- Unauthorized access to sensitive files.  

To further enhance security, I implemented **automated responses** using Wazuh’s Active Response module, which blocked malicious IPs after multiple failed authentication attempts.  



## Conclusion  
This project provided an end-to-end view of cybersecurity, covering both offensive and defensive aspects. Through vulnerability exploitation, lateral movement, and data exfiltration, I was able to demonstrate how attackers operate. On the defensive side, deploying Wazuh SIEM showcased how modern security solutions detect and mitigate threats in real time.  

Moving forward, I plan to refine this lab by testing advanced adversary techniques and improving automated detection strategies. This hands-on experience has significantly strengthened my understanding of enterprise security operations.  



## Special Thanks  
This project was inspired by the incredible work of **Grant Collins**. You can connect with him on LinkedIn [here](https://www.linkedin.com/in/collinsinfosec/), and explore his full project guide on **Building a Cybersecurity Homelab** at [Project Security](https://projectsecurity.teachable.com/p/build-a-cybersecurity-homelab-a-practical-guide-to-offense-defense-enterprise-101).  

Thank you, Grant, for this amazing project and the knowledge you’ve shared! 🚀  


