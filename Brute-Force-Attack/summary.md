#  Brute-force Detection using Wazuh SIEM and Sysmon

##  Summary

This project demonstrates the deployment of a basic SIEM solution using **Wazuh** to detect brute-force login attempts on a Windows system. The environment includes a Wazuh Manager hosted on Ubuntu and a Windows 10 VM acting as the monitored endpoint. Sysmon was installed for advanced logging, and the Wazuh agent was configured to forward logs from Windows to the manager. Custom configurations were applied to monitor Security and Sysmon logs.

---

##  Setup & Configuration

### 1. Wazuh Manager Installation
- Installed Wazuh Manager on an **Ubuntu** virtual machine.
- Verified service status and ensured the dashboard and API were functional.

### 2. Windows Environment Setup
- Installed **Windows 10** in a separate virtual machine.
- Downloaded and installed:
  - **Microsoft Sysmon** (for advanced process logging)
  - **Wazuh Agent** (for log forwarding to the manager)

---

##  Configuration Details

### 3. Sysmon Installation
Sysmon was installed using a community-supported configuration template for maximum event coverage:

```bash
sysmon.exe -accepteula -i sysmonconfig-export.xml
```

### 4. Wazuh Agent Configuration
- The agent was linked to the manager using the `agent-auth` method.
- Verified agent-manager communication by checking the logs:
  ```bash
  tail -f /var/ossec/logs/ossec.log
  ```

---

### 5. Custom `ossec.conf` Configuration (Wazuh Manager)

To monitor logs from the Sysmon, the following configuration was added to ossec.conf in the windoes machine:

```xml
<localfile>
  <location>Microsoft-Windows-Sysmon/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>

<localfile>
  <location>Security</location>
  <log_format>eventchannel</log_format>
</localfile>
```

 This configuration enables real-time monitoring of:

- **Failed login attempts** (Event ID: `4625`)
- **Sysmon process creation** (Event ID: `1`)

---

##  Attack Simulation

### 6. Brute-force Attempt Simulation

On the Windows machine, a brute-force attack simulation was carried out using 10 invalid login attempts via the command prompt:

```cmd
net use \\ip\$ipc /user:username wrongpassword
```

### 7. Log Correlation

- Wazuh successfully captured each failed login attempt in the logs.
- Event ID `4625` was logged for every failure.
- Manual inspection via the Wazuh Dashboard confirmed:
  - The **source IP address** 
  - The **timestamp** of each failed attempt

---

##  Outcome

- **Successful Integration**: Wazuh Manager received and processed security logs from the Windows agent without issue.
- **Accurate Detection**: All failed login attempts were logged and viewable in real-time.
- **Custom Monitoring**: Log channels were properly configured to capture important security-related events.

---

## Tools & Technologies Used

| Tool          | Purpose                                   |
|---------------|-------------------------------------------|
| Wazuh         | SIEM platform                             |
| Sysmon        | System monitoring                         |
| Wazuh agent   | Log forwarding for wazuh                  |
| Windows 10 VM | Attack simulation and log generation      |
| Ubuntu VM     | Hosting the Wazuh Manager                 |

---

## 📁 Files Modified

- `ossec.conf` (on Wazuh Agent):
  - Added `<localfile>` entries to monitor:
    - `Microsoft-Windows-Sysmon/Operational`
    - `Security`


---

