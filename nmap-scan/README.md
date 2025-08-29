# Lab: Nmap Scan 🛡️

## 🔹 Objective
Run an Nmap scan against localhost to identify open ports, services, and potential vulnerabilities.  
The goal is to understand how attackers could exploit exposed services and how defenders can mitigate these risks.

## 🔹 Commands Used nmap 
-sV localhost
nmap --script vuln localhost


## 🔹 Results



Summary of detected open ports:
- **135/tcp open** – MSRPC (Microsoft RPC service)  
- **445/tcp open** – Microsoft-DS (SMB, Server Message Block)  
- **1434/tcp open** – MS-SQL Monitor  
- **1947/tcp open** – Sentinel SRM  
- **3000/tcp open** – PPP  
- **5357/tcp open** – WSDAPI  
- **5432/tcp open** – PostgreSQL database service  
- **7000/tcp open** – AFS3 File Server  
- **8082/tcp open** – BlackIce Alerts  
- **12345/tcp open** – NetBus (historically used as a backdoor Trojan)

Host script results:
- `smb-vuln-ms10-061`: ERROR (could not negotiate connection)  
- `smb-vuln-ms10-054`: false (not vulnerable)  
- `samba-vuln-cve-2012-1182`: connection failed  

## 🔹 Analysis
- Several **critical services** (e.g., SMB on port 445, PostgreSQL on 5432) are running and exposed.  
- Attackers could attempt **brute-force attacks** on PostgreSQL or exploit **SMB vulnerabilities** (e.g., WannaCry ransomware targeted SMB).  
- The presence of port **12345 (NetBus)** is especially concerning — it is historically linked to **remote access Trojans/backdoors**, which could allow attackers full control of the system.  
- Failed script checks show that while some specific SMB exploits didn’t trigger, the services remain exposed and require attention.

## 🔹 Mitigation
- **Firewalling** → Restrict access to only necessary ports/services.  
- **Disable Unused Services** → Ports like 12345 (NetBus) should not be running at all.  
- **Patch Management** → Keep SMB, PostgreSQL, and other services fully updated to avoid known CVEs.  
- **Intrusion Detection (IDS/IPS)** → Monitor repeated login attempts or suspicious scanning activity.  
- **Principle of Least Privilege** → Limit access to services only to authorised users.

## 🔹 Takeaway
This lab shows how a simple Nmap scan can reveal a **lot** about a target system — both legitimate services and dangerous exposures.  
As a defender, regularly scanning your own environment is crucial to **see what attackers see** and close those doors before they are exploited.
