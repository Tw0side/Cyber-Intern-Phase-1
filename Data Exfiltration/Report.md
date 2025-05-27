## Data Exfiltration Detection Using Wazuh

## Set Up

# Victim machine 

To identify exfiltration via PowerShell, we must enable and gather PowerShell logs on the monitored Windows endpoint.

1. Launch PowerShell as an Administrator and execute the following commands to enable PowerShell and script block logging.

2. Insert the following configuration inside the <ossec_config> block of the C:\Program Files (x86)\ossec-agent\ossec.conf file to send PowerShell logs to the Wazuh server for analysis.

<localfile>
  <location>Microsoft-Windows-PowerShell/Operational</location>
  <log_format>eventchannel</log_format>
</localfile>

3. Restart the endpoint to apply the new configuration:

Restart-Computer

# Wazuh-Server

We apply
