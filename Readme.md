# 🔥 Cisco ASA Firewall & DMZ Network Security Project

## 📌 Overview
This project demonstrates a **secure network topology** using a **Cisco ASA 5506-X firewall** to protect internal and DMZ networks. The setup ensures controlled access between the inside, DMZ, and outside networks while enforcing **strong security policies**.

## 🏗️ Network Architecture
- **Inside Network** (192.168.1.0/24) ➝ Internal users.
- **DMZ Network** (192.168.2.0/24) ➝ Public-facing server (e.g., web server).
- **Outside Network** (200.0.0.0/24) ➝ Untrusted external access (e.g., Internet).
- **Router (90.0.0.0/24)** ➝ Simulating external traffic.

## 🔒 Security Features
✅ **Firewall Rules (ACLs):** Restrict inbound/outbound traffic.
✅ **NAT Configuration:** Static NAT for DMZ server, PAT for internal users.
✅ **Security Levels:** Inside (100), DMZ (50), Outside (0).
✅ **Access Control:** Limits admin access using SSH.
✅ **Intrusion Prevention System (IPS):** Detects and blocks malicious traffic.

## 🌍 Real-World Uses & Benefits
### 🔹 **Real-World Applications**
- **Enterprise Security:** Used by organizations to protect their internal network while allowing secure external access to web services.
- **E-Commerce & Banking:** Ensures customer transactions are processed securely via DMZ-hosted applications.
- **Government & Military:** Implements strict access control and monitoring for sensitive data and critical services.
- **Healthcare Systems:** Secures patient records and medical applications with controlled access.
- **Cloud & Hosting Services:** Protects data centers and cloud-hosted applications from cyber threats.

### 🔹 **Benefits of This Network Design**
✅ **Enhanced Security:** Prevents direct access to the internal network by external users.
✅ **Controlled Traffic Flow:** Ensures only authorized connections are permitted between networks.
✅ **Scalability:** Easily expandable to add more servers or security policies.
✅ **Improved Performance:** Reduces the attack surface, allowing faster and more reliable operations.
✅ **Regulatory Compliance:** Helps meet industry standards like PCI DSS, HIPAA, and ISO 27001.

## 🛠️ Configuration Steps
### 🔹 Cisco ASA Firewall Configuration
```cisco
interface GigabitEthernet0/0
 nameif outside
 security-level 0
 ip address 200.0.0.10 255.255.255.0
 no shutdown

interface GigabitEthernet0/1
 nameif inside
 security-level 100
 ip address 192.168.1.1 255.255.255.0
 no shutdown

interface GigabitEthernet0/2
 nameif dmz
 security-level 50
 ip address 192.168.2.1 255.255.255.0
 no shutdown
```

### 🔹 NAT Configuration
```cisco
object network DMZ-SERVER
 host 192.168.2.3
 nat (dmz,outside) static 200.0.0.20
```

### 🔹 Access Control Lists (ACLs)
```cisco
access-list OUTSIDE-TO-DMZ extended permit tcp any host 192.168.2.3 eq 80
access-list OUTSIDE-TO-DMZ extended permit tcp any host 192.168.2.3 eq 443
access-group OUTSIDE-TO-DMZ in interface outside
```

### 🔹 Default Route
```cisco
route outside 0.0.0.0 0.0.0.0 200.0.0.1
```

## 🖥️ PC & Server IP Configuration
| Device | IP Address | Subnet Mask | Default Gateway |
|--------|-----------|-------------|----------------|
| PC0 (Inside) | 192.168.1.3 | 255.255.255.0 | 192.168.1.1 |
| DMZ Server | 192.168.2.3 | 255.255.255.0 | 192.168.2.1 |
| PC1 (Outside) | 90.0.0.3 | 255.255.255.0 | 90.0.0.1 |

## 🚀 How to Run in Cisco Packet Tracer
1. Open **Cisco Packet Tracer**.
2. Build the network as per the diagram.
3. Configure the firewall, router, and end devices.
4. Test **ping and HTTP/HTTPS access** between networks.
5. Adjust ACLs to verify security policies.

## 📢 Contributing
Feel free to **fork**, **clone**, and contribute to improving the security policies and configurations! 🔐

---
🚀 **Developed for Cybersecurity & Networking Enthusiasts** 💻

