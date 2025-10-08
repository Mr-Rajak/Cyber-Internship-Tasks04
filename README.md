# Task 4 - Setup and Use a Firewall

Analyst: Aman Rajak
Date: 2025-09-26
Objective: Configure a local firewall to control network traffic using inbound/outbound rules.

---------------------------------------------------------------------
Tools Used
---------------------------------------------------------------------
- Windows Defender Firewall (for Windows)
- UFW - Uncomplicated Firewall (for Linux)

---------------------------------------------------------------------
Windows Steps Summary
---------------------------------------------------------------------
1. Open Windows Defender Firewall.
2. Go to Advanced Settings -> Inbound Rules.
3. Create a New Rule -> choose Port -> TCP 23 -> Block the connection.
4. Apply rule to all profiles -> name it "Block Telnet".
5. Test with:  telnet localhost 23   (it should be blocked)
6. Delete the rule after test.

---------------------------------------------------------------------
Linux (UFW) Steps Summary
---------------------------------------------------------------------
```bash
sudo ufw status
sudo ufw deny 23
sudo ufw allow 22
sudo ufw status numbered
sudo ufw delete deny 23
```

Explanation:
- Port 23 (Telnet) blocked to prevent insecure access.
- Port 22 (SSH) allowed for secure remote management.
- Screenshots or command outputs were captured as evidence.

---------------------------------------------------------------------
Detailed Explanation of Each UFW Command
---------------------------------------------------------------------

1) sudo ufw status
   Meaning:
     Shows the current status of your firewall (UFW).

   Explanation:
     - If it says "inactive", your firewall is not filtering anything.
     - If it says "active", you will see a list of allowed/denied ports.

   Example output:
```
    Status: active
     To                         Action      From
     --                         ------      ----
     22/tcp                     ALLOW       Anywhere
     23/tcp                     DENY        Anywhere
```
   Behind the scenes:
     Lists all existing firewall rules managed by UFW/iptables.

---------------------------------------------------------------------

2) sudo ufw deny 23
   Meaning:
     Blocks all traffic on port 23 (Telnet).

   Explanation:
     - Any connection attempt on port 23 is rejected.
     - Protects against Telnet, which sends data in plain text.

   Example output:
   ```
     Rule added
     Rule added (v6)
   ```
   Behind the scenes:
     Adds a drop rule in iptables:
       If traffic uses TCP port 23 -> deny it.

---------------------------------------------------------------------

3) sudo ufw allow 22
   Meaning:
     Permits incoming connections on port 22 (SSH).

   Explanation:
     - Allows remote SSH access securely.
     - SSH encrypts communication.

   Example output:
   ```
     Rule added
     Rule added (v6)
   ```
   Behind the scenes:
     Adds a rule in iptables to accept packets on TCP port 22.

---------------------------------------------------------------------

4) sudo ufw status numbered
   Meaning:
     Displays the list of firewall rules with line numbers.

   Explanation:
     - Makes it easier to identify or delete specific rules.
     Example:
```
       Status: active
       To                         Action      From
       --                         ------      ----
       [ 1] 22/tcp                ALLOW       Anywhere
       [ 2] 23/tcp                DENY        Anywhere
```
   Behind the scenes:
     Shows rules in the order UFW applies them.

---------------------------------------------------------------------

5) sudo ufw delete deny 23
   Meaning:
     Removes the rule blocking port 23.

   Explanation:
     - After deletion, port 23 is no longer blocked.
     Example output:
```
       Deleting:
       deny 23/tcp
       Proceed with operation (y|n)? y
       Rule deleted
```
   Behind the scenes:
     Edits iptables to remove the deny entry for TCP port 23.

---------------------------------------------------------------------
How Firewalls Work
---------------------------------------------------------------------
A firewall monitors and controls network traffic based on defined rules.
It acts as a barrier between trusted and untrusted networks, allowing safe
connections and blocking risky ones.

---------------------------------------------------------------------
Deliverables
---------------------------------------------------------------------
- firewall-steps.txt : detailed step-by-step procedure
- report.md          : summary of actions and observations
---------------------------------------------------------------------
