# Course 6: Sound the Alarm - Detection and Response

**Google Cybersecurity Certificate**
**Status: Completed | All Assessments: 100%**

---

## Course Overview

This course covers the full incident response lifecycle, network traffic analysis, detection tools, log management, and SIEM/IDS technologies. It builds the foundational skills needed to detect, investigate, and respond to security incidents as a cybersecurity analyst.

---

## Module 1: Introduction to Detection and Incident Response

**Topics Covered:**

- The NIST Incident Response Lifecycle (Preparation, Detection & Analysis, Containment/Eradication/Recovery, Post-Incident Activity)
- Incident response teams and their roles (CSIRT, SOC)
- Incident response plans and playbooks
- Detection tools: IDS, IPS, EDR
- Documentation tools and their value during incident response
- SIEM (Security Information and Event Management) and SOAR (Security Orchestration, Automation, and Response) tools

**Key Concepts:**

- The difference between events and incidents
- How IDS (Intrusion Detection System) tools monitor and alert on suspicious activity
- How SIEM tools aggregate and correlate log data from multiple sources
- How SOAR tools automate repetitive response tasks

**Graded Assessments:**

- Portfolio Activity: Document an incident with an incident handler's journal — 100%
- Module 1 Challenge — 100%

---

## Module 2: Network Monitoring and Analysis

**Topics Covered:**

- Network traffic flows and the importance of monitoring them
- Data exfiltration attacks and how they appear in network traffic
- Packet structure and packet header fields (IP, TCP, UDP)
- Packet capture tools and techniques
- Wireshark: GUI-based packet analyzer
- tcpdump: command-line packet capture and analysis tool
- Filtering captured packets to identify threats

**Key Concepts:**

- What a packet sniffer (network protocol analyzer) is and how it works
- How to read and interpret packet headers
- How to apply filters in Wireshark and tcpdump to isolate relevant traffic
- The role of packet captures in incident investigation

**Labs:**

- Analyze your first packet (Wireshark)
- Capture your first packet (tcpdump)

**Graded Assessments:**

- Activity: Research network protocol analyzers — 100%
- Module 2 Challenge — 100%

---

## Module 3: Incident Detection, Investigation, and Response

**Topics Covered:**

- The Detection and Analysis phase of the NIST lifecycle
- Cybersecurity incident detection methods
- Indicators of Compromise (IoCs) and how to identify them
- Investigative tools including VirusTotal
- Documentation best practices and chain of custody forms
- Cybersecurity playbooks and their role in standardizing response
- Triage: prioritizing and categorizing alerts
- Containment, Eradication, and Recovery phase
- Business continuity planning during incidents
- Post-incident activity: lessons learned and final reports

**Key Concepts:**

- How IoCs (Indicators of Compromise) help detect breaches
- How to use VirusTotal to analyze suspicious file hashes and URLs
- The purpose of chain of custody documentation in preserving evidence integrity
- How triage helps analysts prioritize alerts under pressure
- What happens during containment, eradication, and recovery
- The importance of post-incident reviews for improving future response

**Graded Assessments:**

- Activity: Investigate a suspicious file hash — 100%
- Activity: Use a playbook to respond to a phishing incident — 100%
- Activity: Review a final report — 100%
- Module 3 Challenge — 100%

---

## Module 4: Network Traffic and Logs Using IDS and SIEM Tools

**Topics Covered:**

- The importance of logs in security monitoring
- Log collection and management best practices
- Log file formats: JSON, CEF, Syslog, and others
- IDS (Intrusion Detection System) detection tools and techniques
- Signature-based vs. anomaly-based detection
- Suricata: open-source IDS/IPS tool
- Writing and examining Suricata detection signatures
- Interpreting Suricata alert and flow logs
- SIEM tools: Splunk and Google SecOps (Chronicle)
- Log ingestion and how SIEM tools process data from multiple sources
- Querying SIEM tools to investigate events
- Wazuh: open-source SIEM and XDR platform

**Key Concepts:**

- How logs serve as the primary evidence trail during an investigation
- The structure of a Suricata rule: action, header, and rule options
- How SIEM tools normalize and correlate log data from different sources
- How to write and run queries in Splunk (SPL) and Google SecOps (YARA-L / UDM)
- How Wazuh provides real-time monitoring, alerting, and log analysis

**Labs:**

- Explore signatures and logs with Suricata
- Perform a query with Wazuh

**Graded Assessments:**

- Activity: Perform a query with Wazuh — 100%
- Module 4 Challenge — 100%
- Portfolio Activity: Finalize your incident handler's journal — 100%

## Certificate

[View Certificate on Coursera] (https://coursera.org/share/a2be04c8ffa4f279e43ebe0ad75fe535)
