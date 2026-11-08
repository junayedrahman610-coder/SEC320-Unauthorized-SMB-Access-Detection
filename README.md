# SEC320 – Unauthorized SMB Access Detection

## Project Overview
This project demonstrates how unauthorized SMB login attempts can be monitored in a virtual cybersecurity lab. I used Kali Linux to simulate failed login attempts against a Windows 10 machine and used Wireshark and Suricata to investigate network traffic.

## Tools Used
- VMware Workstation
- Kali Linux
- Windows 10
- Ubuntu Router
- Nmap
- SMBClient
- Wireshark
- Suricata
- tcpdump

## Network Configuration
| Device | IP Address | Role |
|---|---|---|
| Kali Linux | 10.10.1.5 | Testing machine |
| Ubuntu Router | 10.10.1.1 / 172.16.1.1 | Network routing |
| Windows 10 | 172.16.1.15 | Target machine |
| Suricata VM | Monitoring interface | Traffic monitoring |

## Attack Flowchart
```mermaid
flowchart TD
 A["Kali Linux - 10.10.1.5"] --> B["Nmap Network Scan"]
 B --> C["SMB Service - Port 445"]
 C --> D["SMB Login Attempt"]
 D --> E["Login Failed"]
 D --> F["Traffic Capture"]
 F --> G["Wireshark Analysis"]
 F --> H["Suricata Monitoring"]
 G --> I["Security Investigation"]
 H --> I
 E --> I
 classDef attack fill:#FCE7E7,stroke:#B91C1C,color:#7F1D1D
 classDef monitor fill:#DBEAFE,stroke:#2563EB,color:#1E3A8A
 classDef result fill:#DCFCE7,stroke:#15803D,color:#14532D
 class A,B,C,D,E attack
 class F,G,H monitor
 class I result
```

## Project Steps
### 1. Network Setup
Configured the virtual machines and verified connectivity between Kali Linux and Windows 10 through an Ubuntu router.

### 2. Network Scanning
Used Nmap to identify open services on the Windows machine, including SMB on port 445.

### 3. SMB Login Attempt
Used SMBClient to test unauthorized credentials. The attempt failed with `NT_STATUS_LOGON_FAILURE`.

### 4. Packet Analysis
Used Wireshark to examine SMB2 and NTLMSSP authentication packets.

### 5. Suricata Monitoring
Used Suricata and tcpdump to monitor network activity and review logs. A dedicated Suricata alert for the failed SMB login was not confirmed.

## Results
- Network connectivity was successful.
- Nmap identified open services.
- Unauthorized SMB login attempts failed.
- Wireshark captured authentication traffic.
- Suricata recorded network activity.

## Skills Demonstrated

- Network reconnaissance and service discovery using Nmap
- SMB authentication testing in a controlled lab environment
- Network packet capture and protocol analysis using Wireshark
- Intrusion detection monitoring using Suricata
- Investigation of network traffic and security logs
- Virtual machine networking and troubleshooting
- Cybersecurity documentation and evidence collection


## Conclusion
This project helped me understand how unauthorized login attempts work and how network monitoring tools can help investigate suspicious activity. All testing was completed in an authorized virtual lab for educational purposes.


## Project Screenshots

### 1. Windows Target Configuration

I used Windows 10 as the target machine. I checked its IP address to confirm the network setup.

![Windows Target Configuration](screenshots/Windows%20Victim%20ipconfig.png)

### 2. Network Scanning

I used Kali Linux and Nmap to scan the Windows machine. The scan showed that SMB was running on port 445, along with other open services.

<img width="1919" height="1199" alt="kali ip a ip route nmap -sV 172 16 1 15" src="https://github.com/user-attachments/assets/d0023cd7-f598-400c-828e-f5a062a17f3b" />

### 3. Failed SMB Login Attempt

I used SMBClient to try logging into the Windows machine with incorrect credentials. The login was rejected with NT_STATUS_LOGON_FAILURE.

![Failed SMB Login](screenshots/NT_STATUS_LOGON_FAILURE.png)

### 4. Suricata Monitoring

I started Suricata on the monitoring VM and confirmed that the service was running. I also used tcpdump to capture network traffic.

![Suricata Running](screenshots/active%20%28running%29.png)

### 5. Wireshark Packet Analysis

I opened the captured network traffic in Wireshark and used the ntlmssp filter to examine SMB authentication packets. The packets showed the login attempts from Kali Linux to Windows.

![Wireshark SMB Analysis](screenshots/ntlmssp.png)

### 6. Suricata Logs

I reviewed Suricata's fast.log and JSON event logs to check the recorded network activity. The logs showed network activity, but a specific alert for the failed SMB login was not confirmed.

![Suricata Fast Log](screenshots/fast.log%20contains%20an%20alert.png)

![Suricata JSON Logs](screenshots/JSON%20logs.png)

## Final Summary

In this project, I learned how to test unauthorized SMB login attempts in a virtual lab. I used Nmap to identify services, SMBClient to test authentication, Wireshark to analyze packets, and Suricata to monitor network activity.

The login attempts were unsuccessful, and the captured traffic helped me understand how security teams can investigate suspicious login activity.

All testing was completed in an authorized virtual lab for educational purposes.
