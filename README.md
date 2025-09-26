# UFW_Configuration_Task

1. Enable UFW and List Rules
  Command to Enable: sudo ufw enable
    Output: Firewall is active and enabled on system startup

  Command to List Initial Rules: sudo ufw status verbose
    Initial Rules: Only 80/tcp (Apache) was allowed inbound.
  Default Policy: deny (incoming), allow (outgoing).

2. Add Rule to Block Telnet (Port 23)
    Command to Block: sudo ufw deny 23/tcp
  Output: Rule added (for IPv4 and IPv6)

Verification: sudo ufw status verbose shows 23/tcp with DENY IN.

3. Test the Block Rule
  Command to Test: nc -zvw3 localhost 23
    Output: localhost [127.0.0.1] 23 (telnet) : Connection refused
  Result: The block rule was successful, as the connection was refused.

4. Add Rule to Allow SSH (Port 22)
  Command to Allow SSH: sudo ufw allow 22/tcp
    Output: Rule added (for IPv4 and IPv6)


5. Remove the Test Block Rule
  Command to Remove: sudo ufw delete deny 23/tcp
    Output: Rule deleted (for IPv4 and IPv6)
  Verification: sudo ufw status verbose shows 23/tcp is no longer listed in the rules table.

6. How a Firewall Filters Traffic
    A firewall is essentially a network security system that monitors and controls incoming and outgoing network traffic based on a set of predefined security rules. It acts as a gatekeeper between a trusted internal network (or a single host like your PC) and an untrusted external network (like the internet).

Mechanism of Filtering
1. Rule Set: The firewall maintains an ordered list of rules.

2. Packet Inspection: When a data packet arrives, the firewall immediately inspects its header information. Key inspection points include:

    Source/Destination IP Address: Where the traffic is coming from and going to.
    Port Number: The application or service the traffic is using (e.g., port 23 for Telnet, port 80 for HTTP).
    Protocol: The communication method (e.g., TCP, UDP, ICMP).
    Direction: Whether the traffic is Inbound (entering the host) or Outbound (leaving the host).

3. Rule Matching: The firewall checks the packet against its rules sequentially (top-down).

4. Action Execution:

    If a packet matches a rule (e.g., an inbound packet on port 23 matches the deny 23/tcp rule), the firewall executes the corresponding Action:
    Allow (Accept): The packet passes through.
    Deny (Drop/Reject): The packet is discarded (blocked).

5. Default Policy: If a packet does not match any specific rule, the firewall applies its Default Policy. In UFW setup, the default policy is deny (incoming), meaning anything not explicitly allowed is automatically blocked.
