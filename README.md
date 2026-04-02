# SMB Brute Force and Privilege Escalation Detection using Wazuh SIEM

This project demonstrates a cybersecurity lab focused on detecting SMB brute-force attacks and privilege escalation activities using Wazuh SIEM. The lab simulates an attack from a Kali Linux machine against a Windows system and analyzes how security events are captured and detected.

## Disclaimer
This project was conducted in a controlled lab environment for educational purposes only.

---

## Lab Environment
- Attacker Machine: Kali Linux  
- Target Machine: Windows 10  
- Tools: Nmap, NetExec (nxc), SMBClient, Impacket (psexec), Wazuh  
- Network Type: Host-only / Isolated Network  

---

## Attack & Detection Flow

### 1. Port Scanning
Nmap was used to identify open ports and services on the target machine, revealing SMB services running on port 445.

---

### 2. SMB Brute Force Attack
A brute-force attack was performed using NetExec with username and password wordlists (including rockyou.txt).  
Valid credentials were discovered during the attack:
- Username: Administrator  
- Password: 123456  

---

### 3. Brute Force Detection (Wazuh)
Wazuh SIEM detected multiple failed login attempts (Event ID 4625), indicating a brute-force attack.  
The attack source was identified as:
- Attacker IP: 192.168.0.179  

---

### 4. Shell Access (Remote Execution)
Using valid administrator credentials, remote command execution was performed via Impacket PsExec.  
A remote shell was successfully obtained with elevated privileges:
- NT AUTHORITY\SYSTEM  

---

### 5. Remote Execution Detection
Wazuh detected suspicious service creation and remote execution activity.  
This behavior is mapped to MITRE ATT&CK techniques:
- T1021.002 (SMB/Windows Admin Shares)  
- T1569.002 (Service Execution)  

---

### 6. Privilege Escalation
Privilege escalation was achieved by gaining administrative access and executing commands with SYSTEM-level privileges, demonstrating full control over the target machine.

---

### 7. Detection of Attack Activities
Wazuh SIEM successfully detected:
- Multiple authentication failures (brute force)  
- Successful login after repeated failures  
- Remote service execution (PsExec behavior)  

---

## Key Takeaways
- Weak passwords can lead to full system compromise  
- SMB services are a common attack vector  
- SIEM tools like Wazuh can effectively detect brute-force and lateral movement activities  
- Monitoring Windows Event Logs is critical for identifying attacks  

---

## Screenshots
- Open Ports Scan Result  
- SMB Brute Force Result  
- Detected Attacker IP Address  
- Remote SYSTEM Shell  
- Wazuh Detection Alerts  

---
