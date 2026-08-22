# Home SOC Lab — Wazuh SIEM on Azure

## Overview
A hands-on security operations home lab built on Microsoft Azure to simulate real-world threat detection and incident investigation workflows.

## Architecture
- **Wazuh Server** — Ubuntu 22.04 VM on Azure (North Central US)
- **Windows Agent / Domain Controller** — Windows Server 2022, enrolled as Wazuh agent and promoted to Active Directory Domain Controller (corp.local)
- **Shuffle SOAR** — Cloud-hosted automation platform receiving Wazuh webhooks
- **VirusTotal API** — Threat intelligence enrichment for file hashes
- Both VMs on same Azure Virtual Network (172.16.0.0/24)

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

### Sysmon MITRE ATT&CK mapping
![Sysmon MITRE ATT&CK mapping (T1087)](Sysmon%20MITRE%20ATT%26CK%20mapping%20(T1087)%201.png)
![Sysmon MITRE ATT&CK mapping (T1087)](Sysmon%20MITRE%20ATT%26CK%20mapping%20(T1087)%202.png)
![Sysmon MITRE ATT&CK mapping (T1087)](Sysmon%20MITRE%20ATT%26CK%20mapping%20(T1087)%203.png)

### Privilege escalation detection (Rule 100002)
![Privilege escalation detection](Privilege%20escalation%20detection%20(Rule%20100002)%20.png)

### Domain Admins group changed alert
![Domain Admins group](Domain%20Admins%20group%20changed%20alert%201.png)
![Domain Admins group](Domain%20Admins%20group%20changed%20alert%202.png)
![Domain Admins group](Domain%20Admins%20group%20changed%20alert%203.png)

### IAM user lifecycle
![IAM user lifecycle](IAM%20user%20lifecycle%201.png)
![IAM user lifecycle](IAM%20user%20lifecycle%202.png)

### Shuffle workflow canvas
![Shuffle workflow](Shuffle%20workflow%20canvas.png)

### VirusTotal status
![VirusTotal status](VirusTotal%20status%201.png)
![VirusTotal status](VirusTotal%20status%202.png)

## SOAR Integration
Configured Wazuh to forward alerts with severity ≥10 to Shuffle SOAR 
via webhook. Shuffle automatically queries VirusTotal API for file 
hash reputation, returning results from 75+ antivirus engines including 
malware classification, sandbox verdicts, and threat labels.

## Key Concepts Demonstrated
- SIEM deployment, agent enrollment, and log correlation
- Windows Event Log and Sysmon telemetry analysis (Event ID 1, 4625, 4624)
- Active Directory administration — users, security groups, OUs, RBAC
- Identity and access management — full user lifecycle provisioning and deprovisioning
- Group Policy Object deployment for domain-wide security hardening
- Privilege escalation detection and custom XML rule authoring
- MITRE ATT&CK framework mapping (T1078, T1087, T1098)
- File integrity monitoring using cryptographic checksums
- CIS Benchmark security configuration assessment
- SOAR automation with webhook integration and API orchestration
- VirusTotal API threat intelligence enrichment
- Azure cloud infrastructure (VMs, VNet, NSG, outbound rules)
- Password spraying and brute force attack simulation and detection
