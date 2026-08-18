# Home SOC Lab — Wazuh SIEM on Azure

## Overview
A hands-on security operations home lab built on Microsoft Azure to simulate real-world threat detection and incident investigation workflows.

## Architecture
- **Wazuh Server** — Ubuntu 22.04 VM on Azure (North Central US)
- **Windows Agent** — Windows Server 2022 VM enrolled as monitored endpoint
- Both VMs deployed on the same Azure Virtual Network for agent-manager communication

## Tools Used
- Wazuh SIEM 4.9.2
- Microsoft Azure (Virtual Machines, NSG, VNet)
- Windows Server 2022
- PowerShell

## Attack Simulations & Detections

### 1. Brute Force Authentication Attack
Simulated 10 consecutive failed login attempts using PowerShell net use commands. Wazuh correlated Windows Event ID 4625 entries and fired Rule 60204 (Multiple Windows Logon Failures).

### 2. File Integrity Monitoring
Configured Wazuh FIM to monitor C:\Users\azureuser\Desktop in real time. Created, modified, and deleted a file — triggering Rule 554 (file added), Rule 550 (checksum changed), and Rule 553 (file deleted).

### 3. CIS Benchmark Configuration Assessment
Wazuh automatically ran a CIS Microsoft Windows Server 2022 Benchmark scan against the enrolled endpoint, identifying 222 security misconfigurations across 359 controls with an initial compliance score of 38%.

## Screenshots
### Wazuh Dashboard
![Wazuh Dashboard](Wazuh%20Dashboard.png)

### Windows Agent Enrolled
![Windows Agent Enrolled](Windows%20Agent%20Enrolled.png)

### Brute Force Detection Alerts
![Brute Force Alerts](Brute%20Force%20Alerts.png)

### File Integrity Monitoring Alerts
![FIM Alerts](FIM%20Alerts.png)

### CIS Benchmark Assessment
![CIS Benchmark](CIS%20Benchmark.png)

## In Progress
- Sysmon integration for enriched Windows telemetry
- Custom Wazuh detection rules mapped to MITRE ATT&CK framework
- Active Directory Domain Controller deployment
- AD attack simulation (Kerberoasting, AS-REP roasting)
- Active response scripts for automated threat containment

## Key Concepts Demonstrated
- SIEM deployment and agent enrollment
- Windows Event Log correlation and brute force detection
- File integrity monitoring using cryptographic checksums
- CIS Benchmark security configuration assessment
- Azure cloud infrastructure (VMs, VNet, NSG configuration)
