# Professional Report on Suspicious Network Activity Detection Using Wireshark

## Introduction

In today’s digital landscape, the monitoring of network traffic for suspicious activities has become increasingly crucial for maintaining network security. This report outlines a simulation conducted to detect suspicious network activity using the Wireshark tool, specifically focusing on the identification of SYN scans, a common reconnaissance technique employed by attackers.

## Setup

To effectively perform the simulation, the following setup was implemented:

1. **Wireshark Installation**: The Wireshark tool was installed on the victim machine to monitor incoming and outgoing network traffic.
2. **Port Scanning Simulation**: The attack machine, equipped with Nmap, was utilized to simulate a port scanning attack.
3. **SYN Scanning**: For this scenario, a SYN scan was selected due to its stealthy nature and common use in penetration tests.

## Simulation Procedure

The following steps were taken to conduct the simulation:

1. **Initiate Nmap Scan**: The attacker machine was accessed via a terminal, where the command `nmap -sS [IPADDRESS]` was executed. This command initiates a SYN scan on the specified target IP address, attempting to identify open ports without establishing a full TCP connection.

2. **Launch Wireshark**: Concurrently, Wireshark was opened on the victim machine, where the appropriate network interface was selected for traffic monitoring.

3. **Traffic Monitoring**: Wireshark began listening for all network traffic, capturing packets to analyze later.

4. **Apply Custom Filter**: To streamline the detection of suspicious activity, a filter was applied in Wireshark: `tcp.flags.syn == 1 and tcp.flags.ack == 0`. This filter specifically isolates SYN packets that are sent without corresponding ACK packets, indicating incomplete handshake attempts typical of SYN scans.

## Findings

The application of the specified filter revealed instances of suspected SYN scanning activity. Such behavior is considered malicious, as it suggests an unauthorized attempt to probe the network for vulnerabilities without the typical exchange that occurs during a legitimate connection establishment.

## Recommendations

In light of the findings from this simulation, it is imperative to implement the following measures to enhance network security:

- **Firewall Configuration**: Establish robust firewall rules to detect and mitigate unauthorized scanning attempts. 
- **Intrusion Detection Systems (IDS)**: Utilize IDS to monitor network traffic continuously and alert administrators of suspicious activities.
- **Regular Monitoring**: Conduct frequent audits and scans of network traffic to identify potential threats promptly.

## Conclusion

Monitoring network traffic for suspicious activity is essential in safeguarding systems against potential threats. This simulation successfully demonstrated the use of Wireshark in detecting SYN scans, emphasizing the need for proactive measures to prevent unauthorized access and maintain the integrity of network infrastructure. Implementing strong security protocols will ensure better protection against potential cyber threats. 

By adhering to the recommendations outlined in this report, organizations can bolster their network security posture and respond effectively to potential vulnerabilities.
