# Cisco-RIP-Configuration
Hands-on Cisco RIPv2 configuration lab demonstrating dynamic routing between New York (NY) and Los Angeles (LA) routers. Includes RIP Version 2 configuration, routing table verification, network advertisement, and successful end-to-end connectivity testing with 0% packet loss.

Network Topology

The lab consists of two Cisco routers connected through a shared transit network.
Device	Interface	IP Address	Network
Router 1 (NY)	G0/0	192.168.20.1	192.168.20.0/24
Router 1 (NY)	G0/1	192.168.10.1	192.168.10.0/24
Router 2 (LA)	G0/0	192.168.20.2	192.168.20.0/24
Router 2 (LA)	G0/1	192.168.30.1	192.168.30.0/24
Network Diagram
text

         New York (NY) Router
                NY
                 |
         G0/1    |    G0/0
    192.168.10.1 | 192.168.20.1
                 |
          192.168.20.0/24
                 |
         G0/0    |    G0/1
    192.168.20.2 | 192.168.30.1
                 |
         Los Angeles (LA)
                 |
          192.168.30.0/24
                 |
           Destination Network
             192.168.30.0/24

Technologies Used

    Cisco IOS
    Cisco Routers
    Routing Information Protocol (RIP)
    RIPv2
    IPv4 Addressing
    Dynamic Routing
    ICMP (Ping)
    Cisco Command Line Interface (CLI)

RIP Configuration

Both routers were configured to use RIPv2 to exchange routing information across their connected networks.
1. Router 1 – New York (NY)

Enter privileged EXEC mode and global configuration mode.
NY> enable
NY# conf t

Enable the RIP routing process.

NY(config)# router rip

Specify RIPv2.

NY(config-router)# version 2

Advertise the connected networks.

NY(config-router)# network 192.168.10.0
NY(config-router)# network 192.168.20.0

Verify the routing table.

NY(config-router)# do show ip route

NY Routing Table Results:

    192.168.10.0/24 – Directly connected.
    192.168.20.0/24 – Directly connected.

The New York router advertises both networks through RIPv2 so that the Los Angeles router can dynamically learn the remote network.

2. Router 2 – Los Angeles (LA)

Enter privileged EXEC mode and global configuration mode.

LA> enable
LA# conf t

Enable the RIP routing process.

LA(config)# router rip

Specify RIPv2.

LA(config-router)# version 2

Advertise the connected networks.

LA(config-router)# network 192.168.20.0
LA(config-router)# network 192.168.30.0

Verify the routing table.

LA(config-router)# do show ip route

LA Routing Table Results:

    192.168.20.0/24 – Directly connected.
    192.168.30.0/24 – Directly connected.
    192.168.10.0/24 – Learned through RIP.

The following routing table entry confirms that LA successfully learned the New York network through RIPv2:
text

R 192.168.10.0/24 [120/1] via 192.168.20.1,
  GigabitEthernet0/0

The routing code R identifies a route learned through RIP.
Routing Table Verification

The routing tables confirm that the routers successfully exchanged routing information.
Understanding Routing Table Codes
Code	Meaning
C	Directly Connected
L	Local Interface Address
R	RIP Learned Route
O	OSPF Learned Route
S	Static Route
Understanding the RIP Route
text

R 192.168.10.0/24 [120/1] via 192.168.20.1

    R: Route learned through RIP.
    192.168.10.0/24: Destination network.
    120: RIP administrative distance.
    1: RIP hop count (metric).
    192.168.20.1: Next-hop router (NY).

This confirms that the LA router learned how to reach the New York network through the NY router using one hop.
Connectivity Testing

After completing the RIPv2 configuration, an ICMP ping test was performed to verify end-to-end network connectivity.

Test Destination: 192.168.10.10

Command:
text

ping 192.168.10.10

Ping Test Results
text

Pinging 192.168.10.10 with 32 bytes of data:

Reply from 192.168.10.10: bytes=32 time=6ms TTL=126
Reply from 192.168.10.10: bytes=32 time<1ms TTL=126
Reply from 192.168.10.10: bytes=32 time=4ms TTL=126
Reply from 192.168.10.10: bytes=32 time<1ms TTL=126

Ping statistics for 192.168.10.10:
    Packets: Sent = 4,
    Received = 4,
    Lost = 0 (0% loss),

Approximate round trip times in milli-seconds:
    Minimum = 0ms,
    Maximum = 6ms,
    Average = 2ms

Ping Test Summary
Metric	Result
Destination IP	192.168.10.10
Packets Sent	4
Packets Received	4
Packets Lost	0
Packet Loss	0%
Minimum Response Time	0ms
Maximum Response Time	6ms
Average Response Time	2ms

Result: Successful connectivity.

All four ICMP packets received responses, confirming successful communication with the destination host.
RIP Verification Commands

The following Cisco IOS commands can be used to verify RIP operation and routing information.
cisco

show ip route
show ip protocols
show ip rip database
show running-config

Command	Purpose
show ip route	Displays the routing table
show ip protocols	Displays active routing protocols
show ip rip database	Displays RIP routing information
show running-config	Displays the current router configuration
Project Results

The RIPv2 configuration was successfully implemented between the New York and Los Angeles routers.

The following objectives were achieved:

    Configured RIP routing on both Cisco routers.
    Enabled RIPv2 using the version 2 command.
    Advertised connected networks through RIP.
    Successfully exchanged routing information.
    Verified dynamically learned routes using show ip route.
    Confirmed the remote New York network was learned by the Los Angeles router.
    Completed an end-to-end ping test with 0% packet loss.

Conclusion

This lab demonstrates how RIPv2 enables dynamic routing between separate networks using Cisco routers.

By configuring RIP on the New York and Los Angeles routers, the devices successfully exchanged routing information and dynamically learned remote network routes.

The routing table verification confirmed that the Los Angeles router learned the New York network through RIP with an administrative distance of 120 and a hop count of 1.

Finally, the successful ping test to 192.168.10.10, with four packets transmitted and zero packets lost, demonstrated end-to-end network connectivity.

This project provided hands-on experience with Cisco IOS, RIPv2 configuration, dynamic routing, routing table analysis, and network connectivity troubleshooting.

Project Name: Cisco-RIP-Configuration
Routing Protocol: RIP
Version: RIPv2
Routers: New York (NY) and Los Angeles (LA)
Connectivity Test: Successful (0% Packet Loss)

