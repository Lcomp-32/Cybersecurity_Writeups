## Lab Overview

**Lab:** Packet Detective  \
**Objective:** Analyze network traffic in PCAP files using Wireshark to extract IOCs and reconstruct attacker tactics like authentication and remote execution.

## Tools & Environment

**OS:** Ubuntu  \
**Tools:** Wireshark  \
**Targets:** 172.16.66.37 & 172.16.66.36

## Threat Vulnerability Summary

**Vulnerability:** Compromise of a priviledged account; Suspicious SMB traffic \
**Risk Level:** high - Bad actor currently is exploiting the privilege of a compromised account  \
**Impact:** high - This leads to remote access to many systems allowing data exfiltration or compromising devices

#### Collection

Packet sniffer produced .pcapng files of suspicious activity. 
#### Analysis

Inital reveiew of the .pcapng files revealed an unusually high amount of SMB traffic in a short timeframe. Upon review of the SMB authentication packets, the user *administrator* is found to be the one making the requests which is a highly priviledged account. Inspecting the tree connect requests revealed that the file /eventlogs had a WRITE operation during the time of the suspicious traffic. The timestamp of this traffic anchors our timeline to 9-23-2020 at 16:50. The WRITE operation is especially concerning because it aligns with anti-forensic behavior. This is most likely an attempt to destroy evidence of prior activity.

The SMB requests require further review because of the sensitive systems that this user can access.\

#### IOC Extraction

| Indicator | Type | Value | Timestamp |
| --------- | ---- | ----- | --------- |
| blank | blank | blank | blank |


Using the protcol hierachry statistics tool on the first file, extensive data transfer was shown with 4406 bytes. Upon looking into the packets reguarding authentication using SMB shows the username was used, Administrator. Looking further into the SMB traffic a file was accessed, /eventlog. This allows me to infer the modivations for the bad actor. Most likely the bad actor was trying to modify or clear eventlogs to hide other exploits preformed. The first write traffic for /eventlogs happened at 9-23-2020 at 16:50. This gives us a timeline for the bad actors actions and the logs that they erased. 

#### Remediation & Mitigation
