
**Firewall Configuration Report**


Analyst: Aman Rajak

Date: 2025-09-26

Task: Setup and Use a Firewall

Platform: Windows / Linux (UFW)

--------------------------------------------------------------
Summary
--------------------------------------------------------------
A basic firewall configuration was performed to test rule creation and verification. The goal was to block port 23 (Telnet), an insecure service, and confirm the system correctly denied access.

--------------------------------------------------------------
Steps Performed
--------------------------------------------------------------
Step | Action                      | Command/Tool                    | Result
-----|-----------------------------|---------------------------------|--------------------------------------------
1    | Checked current firewall    | sudo ufw status / Firewall GUI  | Confirmed firewall was active
2    | Blocked port 23 (Telnet)    | sudo ufw deny 23 / New rule     | Connection attempts were denied
3    | Tested the block            | telnet localhost 23             | Failed to connect (as expected)
4    | Allowed SSH (Linux only)    | sudo ufw allow 22               | Verified SSH access works
5    | Deleted block rule          | sudo ufw delete deny 23         | Firewall restored to normal state
6    | Took screenshots            | (manual step)                   | Stored in /screenshots directory

--------------------------------------------------------------
Observations
--------------------------------------------------------------
- Blocking port 23 successfully prevented Telnet connections.
- Allowing port 22 preserved secure remote access.
- Firewall rules worked as expected and were easy to manage using both command-line (UFW) and GUI tools (Windows Firewall).

--------------------------------------------------------------
Concept Summary
--------------------------------------------------------------
A firewall filters packets entering or leaving a system based on defined rules. It enforces network security by allowing only approved ports and blocking potentially dangerous services such as Telnet.

Types of firewall rules:
- Inbound Rules  : Control traffic coming into your device.
- Outbound Rules : Control traffic leaving your device.

--------------------------------------------------------------
Risk Justification
--------------------------------------------------------------
Telnet (port 23) transmits usernames and passwords in plain text, making it easy for attackers to intercept sensitive information. SSH (port 22) replaces Telnet and provides encrypted communication, protecting confidentiality and integrity of data in transit.

--------------------------------------------------------------
Conclusion
--------------------------------------------------------------
The firewall test confirmed that the system is capable of blocking insecure services effectively. Proper firewall configuration remains a critical first line of defense in any cybersecurity environment.
--------------------------------------------------------------
