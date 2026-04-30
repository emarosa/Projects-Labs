# Nmap Lab

## Objective
The goal of this lab was to move beyond simple connectivity and do some packet inspection to identify  software versions running on the victim device. This data is then used to map services to known CVEs.

## Execution
I used Nmap with the -sV and -sC  flags. This allowed me to pull version banners from the target's open ports to identify outdated or insecure software.

### **Target Information**
* **Target IP:** `10.0.2.5`
* **Scan Command:** `sudo nmap -sV -sC -Pn 10.0.2.5`

### **Full Service Scan Results**
| Port | Protocol | Service | Version | Risk Level |
| :--- | :--- | :--- | :--- | :--- |
| 21 | tcp | ftp | **vsftpd 2.3.4** |  Critical |
| 22 | tcp | ssh | OpenSSH 4.7p1 |  Medium |
| 23 | tcp | telnet | Linux telnetd |  High |
| 80 | tcp | http | Apache httpd 2.2.8 |  High |
| 445 | tcp | netbios-ssn | Samba smbd 3.X | Medium |
| 3306 | tcp | mysql | MySQL 5.0.51a | Medium |
| 1524 | tcp | ingreslock | Bindshell (Root) | Critical |

---

## Target : Port 21 (vsftpd 2.3.4)
While many ports are open, Port 21 stood out as a bigggg vulnerability. The scan identified the version as `vsftpd 2.3.4`.

### **Research **
 researching this specific version, I identified a famous supply-chain attack:
* **CVE ID:** [CVE-2011-2523](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2011-2523)
* **Vulnerability Type:** Backdoor Command Execution.
* **Description:** This version of vsftpd contains a malicious backdoor that allows for unauthorized root access if a specific string (`:)`) is included in the username during login.

---

##  Lab Evidence
<p align="left">
 <video src="./Nmap-Lab-Video/Nmaplab" width="90%" />
</p>

---

##  Conclusion
By doing this scan, I  mapped an open port to a verified critical vulnerability. This shows the transition from network discovery to vulnerability research.
