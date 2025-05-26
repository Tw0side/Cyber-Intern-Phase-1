# Windows Brute-force Detection using Wazuh SIEM and Sysmon

##  Overview

As part of my internship task, I implemented a Security Information and Event Management (SIEM) solution using **Wazuh** to detect brute-force login attempts on a Windows system. This involved setting up the Wazuh server, configuring agents, integrating Microsoft Sysmon for detailed telemetry, and customizing log collection and analysis to correlate failed login events.

---

##  Setup & Configuration

### 1. **Wazuh SIEM Installation**
- Installed **Wazuh Manager** on an Ubuntu virtual machine.
- Verified successful installation using Wazuh dashboard and command-line tools.

### 2. **Windows Environment Preparation**
- Set up a Windows 10 virtual machine.
- Installed the following components:
  - **Microsoft Sysmon** for advanced system activity monitoring.
  - **Wazuh Agent** to forward logs to the Wazuh Manager.

---

##  Configuration Details

### 3. **Sysmon Installation**
- Sysmon was installed using the SwiftOnSecurity configuration template:
  ```bash
  sysmon.exe -accepteula -i sysmonconfig-export.xml

