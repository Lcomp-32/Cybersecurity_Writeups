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

## Methdology

#### Reconnaissance
While looking at the .pcapng files in wireshark, I saw many SMB and SMB2 requests that was flagged as suspcious. Three artifacts were saved and were ready to view. 

#### Vulnerability Analysis

This vulnerability can have negative ramifications for all devices in the network that the account has additional priviledges to.

#### Exploitation

#### Post-Exploitation

#### Evidence & Logs

Using the protcol hierachry statistics tool on the first file, extensive data transfer was shown with 4406 bytes. Upon looking into the packets reguarding authentication using SMB shows the username was used, Administrator. Looking further into the SMB traffic a file was accessed, /eventlog. This allows me to infer the modivations for the bad actor. Most likely the bad actor was trying to modify or clear eventlogs to hide other exploits preformed. The first write traffic for /eventlogs happened at 9-23-2020 at 16:50. This gives us a timeline for the bad actors actions and the logs that they erased. 

#### Remediation & Mitigation
