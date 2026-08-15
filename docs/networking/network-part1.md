***Data Transmission***

•	-Guided Transmission Media (Wired Media) 

o	-Twisted Pair Cable (Copper Cable) 

o	-Coaxial Cable 

o	-Printed Circuit Board (PCB) Traces 

o	-Fiber Optic Cable 

**Unguided Transmission Media (Wireless Media)**

o	Radio Waves

o	Bluetooth 

•	Types of Signals

o	Analog Signal 

o	Digital Signal 

**What is a Modem?** 

o	A modem performs modulation and demodulation: 

	Modulation: Converts a digital signal into an analog signal for transmission. 

	Demodulation: Converts an analog signal back into a digital signal after reception. 

**More professional version (suitable for interviews or study notes)Data Transmission**

1.Guided Transmission Media (Wired Communication)

o	Copper Cable (Twisted Pair) 

o	Coaxial Cable 

o	Printed Circuit Board (PCB) Traces

o	Fiber Optic Cable

2.Unguided Transmission Media (Wireless Communication)

o	Radio Waves  
o	Bluetooth

3.Types of Signals

o	Analog Signal  
o	Digital Signal  
4.Modem  
oA modem (Modulator-Demodulator)  is a device that converts digital data into analog signals for transmission and converts received analog signals back into digital data.  
o	Modulation: Digital → Analog  
o	Demodulation: Analog → Digital


**Bandwidth**: Bandwidth is the maximum amount of data that can be transmitted over a network connection in a given amount of time. It is usually measured in bits per second (bps), such as:

•	Kbps = Kilobits per second   
•	Mbps = Megabits per second    
•	Gbps = Gigabits per second 

**Throughput** : Throughput is the actual amount of data that is successfully transmitted over a network in a given period of time.     

**What is an IP Address?**

An IP (Internet Protocol) address is a unique identifier assigned to a device on a network.

**It has two main purposes:**
1.	Identify a device. 
2.	Locate the device so data can be delivered correctly. 

**Think of it like a home address**:

•	Country → Network   
•	Street → Subnet   
•	House number → Host   
**Example**:  
192.168.1.25

***IPv4***

IPv4 is the 4th version of the Internet Protocol.   
•	32-bit address   
•	Four decimal numbers separated by dots   
•	Each number ranges from 0 to 255   
**Example**:  
192.168.10.25

***IPv6*** 

IPv6 was introduced because IPv4 addresses are limited.  
Features:  
•	128-bit address   
•	Written in hexadecimal   
•	Eight groups separated by colons      
**Example**:  
2001:0db8:85a3:0000:0000:8a2e:0370:7334

**IPv6 supports approximately  
2^128**

Advantages:  
•	Huge address space   
•	Better routing   
•	Built-in IPsec support   
•	No need for NAT in many deployments   
•	Simpler automatic configuration

**Broadcast**    
Broadcast means sending one packet to every device on the same network.  
Instead of sending data to one computer:  
PC1 → PC2  
Broadcast sends it to everyone:  
           PC2  
          /  
PC1 ---- Switch  
       \   
        PC3  
         \  
          PC4    
Common uses:  
•	ARP requests   
•	DHCP Discover messages   
**Broadcast Address**  

A broadcast address is the last IP address in a subnet.     
Example:  
Network:  
192.168.1.0/24  
Range:  
Network Address:    192.168.1.0  
First Host:         192.168.1.1  
Last Host:          192.168.1.254  
Broadcast Address:  192.168.1.255 

**Does IPv6 Have Broadcast?**
No.  
IPv6 does not support broadcast.  
Instead, IPv6 uses multicast.  
For example, instead of broadcasting to every device, IPv6 sends packets only to devices that are interested in receiving them.  
**Multicast**  
Multicast means sending data to a specific group of devices, rather than to one device (unicast) or every device (broadcast).  
Quick way to remember  
•	**IP Address** = A device's unique   network address.   
•	**IPv4** = 32-bit addresses (e.g., 192.168.1.10).   
•	**IPv6** = 128-bit addresses (e.g., 2001:db8::1).   
•	**Broadcast** (IPv4 only) = Send to everyone on the local network.   
•	**Multicast** = Send to only a selected group of devices.   
•	**Unicast** = Send to one specific device.  

**What is a Loopback Address?**

A loopback address is a special IP address that a device uses to communicate with itself. Any packet sent to a loopback address never leaves the device—it is sent back internally by the operating system.    

Think of it as calling your own phone number. The communication never goes out to the network.  
***IPv4 Loopback***  
The most common IPv4 loopback address is:  
**127.0.0.1**  
***IPv6 Loopback***  
IPv6 has a single loopback address:    
**::1**

**Why Is It Used?**
1. Testing the TCP/IP Stack
Check whether networking is working on your own machine.  
Linux:  
ping 127.0.0.1  
or  
ping localhost  
If this fails, there's a problem with your local networking stack
TCP (Transmission Control Protocol)
TCP is a connection-oriented protocol that ensures data is delivered reliably and in the correct order.

Before sending data, TCP establishes a connection between the sender and receiver.  
Features of TCP  
•	✅ Reliable delivery   
•	✅ Error checking   
•	✅ Retransmits lost packets   
•	✅ Delivers packets in the correct order   
•	✅ Flow control (prevents overwhelming the receiver)   
•	✅ Congestion control (reduces traffic when the network is busy)
How TCP Works ?  
TCP uses a Three-Way Handshake to establish a connection:  
Client                  Server  
   | ---- SYN --------> |  
   | <--- SYN-ACK ----- |  
   | ---- ACK --------> |  
Common TCP Applications  
•	HTTP / HTTPS (Web browsing)   
•	SSH (Remote login)   
•	FTP (File Transfer)   
•	SMTP (Email)   
•	IMAP / POP3 (Email retrieval)   
•	SQL database connections  
UDP (User Datagram Protocol)  
UDP is a connectionless protocol.    

It sends data without establishing a connection and does not guarantee delivery, order, or error recovery.    
Features of UDP  
•	✅ Very fast   
•	✅ Low overhead   
•	❌ No retransmission   
•	❌ No delivery guarantee   
•	❌ No packet ordering   
•	❌ No flow control  


Easy way to remember  
•	TCP = "Accuracy first." Reliable, ordered, and guaranteed delivery.   
•	UDP = "Speed first." Minimal overhead and ideal for real-time   communication where occasional packet loss is acceptable.  
**The 7 OSI Layers**    
Layer  	Name	 Main Function	  Examples

7	Application	Provides network services to applications	HTTP, HTTPS, FTP, SMTP, DNS  

6	Presentation	Data formatting, encryption, compression	SSL/TLS, JPEG, ASCII, UTF-8

5	Session	Establishes and manages communication sessions	 NetBIOS, RPC

4	Transport	Reliable data delivery	TCP, UDP

3	Network	Logical addressing and routing	IP, ICMP, Routers

2	Data Link	Physical addressing and error detection	Ethernet, MAC, Switches

1	Physical	Transmits raw bits over the medium	Cables, Fiber, Wi-Fi signals   
**Layer 7 – Application**  
This is the layer closest to the user.  
It provides network services to   applications like:  
•	Web browsers   
•	Email clients   
•	FTP clients   
Common Protocols  
•	HTTP   
•	HTTPS   
•	FTP   
•	SMTP   
•	DNS   
•	SSH  

**Layer 6 – Presentation**  
This layer prepares data for the application.  
Its responsibilities include:  
•	Data formatting   
•	Encryption   
•	Decryption   
•	Compression  
**Layer 5 – Session**  
This layer manages communication sessions.
Responsibilities:  
•	Start a session   
•	Maintain it   
•	End it  
**Layer 4 – Transport**  
This layer ensures applications can communicate reliably (or quickly).    
Protocols:  
•	TCP   
•	UDP   
Responsibilities:  
•	Segmentation   
•	Error recovery   
•	Flow control   
•	Reliability   
•	Port numbers  
**Layer 3 – Network**  
The Network layer is responsible for routing packets between different networks.  
Responsibilities:  
•	IP addressing   
•	Routing   
•	Packet forwarding   
Protocols:  
•	IPv4   
•	IPv6   
•	ICMP  
**Layer 2 – Data Link**  
This layer delivers data between devices on the same local network (LAN).  
Responsibilities:  
•	MAC addressing  
•	Error detection   
•	Framing   
Protocols:  
•	Ethernet   
•	Wi-Fi (IEEE 802.11)   
Device:  
•	Switch    
**Layer 1 – Physical**  
This layer transmits raw bits.  
Examples:  
•	Copper cable   
•	Fiber optic cable   
•	Radio waves   
•	Network connectors (RJ45)   
Devices:  
•	Hub   
•	Repeater   
•	Cables  

Devices at Each Layer  
Device	OSI Layer
Hub	Layer 1  
Repeater	Layer 1  
Switch	Layer 2  
Bridge	Layer 2  
Router	Layer 3  
Firewall (traditional)	Layer 3/4  
Load Balancer	Layer 4/7  
Proxy Server	Layer 7  
Easy Mnemonic  
From Layer 7 → Layer 1:  
All People Seem To Need Data Processing  
•	A → Application  
•	P → Presentation   
•	S → Session  
•	T → Transport  
•	N → Network   
•	D → Data Link  
•	P → Physical  
**Or from Layer 1 → Layer 7:**   
Please Do Not Throw Sausage Pizza Away   
•	P → Physical  
•	D → Data Link  
•	N → Network  
•	T → Transport  
•	S → Session  
•	P → Presentation  
•	A → Application  
	Bits
***What is a Router?***  
A router is a device that connects different networks and forwards packets between them.  
Its main job is to determine the best path for data using IP addresses.  
Example

Your router connects:  
•	Your local network (LAN)   
•	The Internet (WAN)   
When your computer wants to access Google, it sends the packet to the router, which forwards it toward Google's network.  
Responsibilities of a Router  
•	Connect different networks   
•	Forward IP packets   
•	Maintain routing tables   
•	Choose the best route   
•	Often perform NAT (Network Address   Translation)   
**OSI Layer**  
A router primarily operates at Layer 3 (Network Layer).  
**What is a Gateway?**  
A gateway is a device or software that acts as an entry and exit point between one network and another.   
In everyday networking, the term default gateway usually refers to the router that your computer sends traffic to when the destination is outside the local network.  
Example
Suppose your PC has:
IP Address:       192.168.1.10  
Subnet Mask:      255.255.255.0  
Default Gateway:  192.168.1.1  

***What is Network Topology?***  
A network topology is the physical or logical layout of devices and connections in a network. 
 
**Types of Network Topology**
There are six common network topologies:
1.	Bus Topology 
2.	Star Topology 
3.	Ring Topology 
4.	Mesh Topology 
5.	Tree Topology 
6.	Hybrid Topology  
**Enterprises**
Hybrid	Varies	High	Very High  	Large organizations  
Easy Way to Remember  
•	Bus → One shared cable.   
•	Star → Everything connects to one central switch. ⭐   
•	Ring → Devices form a circle. ⭕   
•	Mesh → Everyone connects to   everyone. 🕸️   
•	Tree → Hierarchical branches. 🌳   
•	Hybrid → A combination of   multiple topologies.    
**What is a Port?**  
A port is a logical communication endpoint used by applications and services on a computer.  
Port	Protocol	Service  
20/21	TCP	FTP  
22	TCP	SSH  
23	TCP	Telnet  
25	TCP	SMTP  
53	TCP/UDP	DNS  
67/68	UDP	DHCP  
80	TCP	HTTP  
110	TCP	POP3  
123	UDP	NTP  
143	TCP	IMAP  
161	UDP	SNMP  
443	TCP	HTTPS  
Registered Ports (1024–49151)  
Assigned to specific applications.  
Examples:  
•	1433 → Microsoft SQL Server   
•	3306 → MySQL   
•	5432 → PostgreSQL   
•	6379 → Redis   
•	8080 → Alternative HTTP  
TCP and UDP Ports  
Both TCP and UDP use port numbers, but   independently.  
For example:  
53/TCP  
53/UDP  
Common DevOps Ports  
Service	Port  
SSH	22  
HTTP	80  
HTTPS	443  
Docker Registry	5000  
Jenkins	8080  
GitLab	80 / 443  
Kubernetes API	6443  
Prometheus	9090  
Grafana	3000  
Elasticsearch	9200  
Kibana	5601  
Zabbix Server	10051  
Zabbix Agent	10050  
**Summary**  
Concept	Description  
IP Address	Identifies a device on the network  
Port	Identifies an application or service on that device  
TCP/UDP	Transport protocols that use ports
Socket	IP + Port + Protocol  
NAT (Network Address Translation) is a networking technique used by a router or firewall to translate one IP address into another as packets pass between networks.  
**Why do we need NAT?**  
Private IP addresses (such as 192.168.x.x, 10.x.x.x, and 172.16.x.x – 172.31.x.x) cannot be used directly on the Internet.  
NAT solves this problem by:  
•	Conserving public IPv4 addresses   
•	Hiding internal network addresses   
•	Allowing many devices to access the     Internet through a single public IP  

All three devices access the Internet simultaneously using the same public IP, and the router uses PAT to distinguish their traffic.  
Both tcpdump and Wireshark are packet capture (packet sniffer) tools. They let you see the network traffic flowing through a network interface, which is essential for troubleshooting connectivity, performance, and security issues.  
The main difference is:  
•	tcpdump → Command-line tool (great for Linux servers and SSH sessions)    
•	Wireshark → Graphical tool (great for analyzing packets in detail)   
important tcpdump commands:  
```tcpdump -D```  
```sudo tcpdump -i eth0```  
```sudo tcpdump -i any```  
```sudo tcpdump -n```  
```sudo tcpdump -c 100```      
```sudo tcpdump -i eth0 -w capture.pcap```    
```sudo tcpdump host 192.168.1.100```  
```sudo tcpdump dst 8.8.8.8```  
```sudo tcpdump udp```  
```sudo tcpdump port 53```  
```sudo tcpdump 'port 80 or port 443'```

 
```Ifconfig```  
```ifconfig [interface] [options]```  
```ifconfig -a```  
```sudo ifconfig eth0 192.168.1.100 netmask 255.  255.255.0```  
```sudo ifconfig eth0 up```  
```sudo ifconfig eth0 down```    

***MTU***   
(Maximum Transmission Unit) is the largest packet (frame payload) size, measured in bytes, that a network interface can send in a single transmission without fragmentation  
Example  
Suppose the MTU is 1500 bytes.  
Packet Size = 1400 bytes  
MTU         = 1500 bytes  
✔ Packet is sent normally.  
```Ip add show```  
***nmcli***  
 (NetworkManager Command Line Interface) is a command-line tool used to configure, manage, and troubleshoot network connections on Linux systems that use NetworkManager.  
It lets you manage:  
•	Ethernet connections   
•	Wi-Fi   
•	Static IP addresses   
•	DHCP   
•	DNS   
•	Gateways   
•	VPNs   
•	Network interfaces   

It is the command-line equivalent of the graphical NetworkManager application.   
```systemctl status NetworkManager```   
```sudo systemctl enable NetworkManager```  
**Example:**  
DEVICE         TYPE         STATE          CONNECTION   
eth0        ethernet  connected  Wired connection 1  
wlan0       wifi      disconnected --  
lo          loopback  unmanaged  --   
```nmcli connection show```  
```nmcli connection down [name of connection]```
```nmtui > graphical network manager```  
***Name Resolution in Networking***    
Name resolution is the process of translating a human-readable hostname (domain name) into an IP address that computers use to communicate.   
For example:  
www.google.com  
        ↓  
142.250.190.78    
Humans remember names like google.com, but computers communicate using IP addresses.
Why Do We Need Name Resolution?  
Imagine opening a browser and typing:  
www.github.com  
Your computer cannot connect using the name alone.  
It first needs to find the IP address:  
www.github.com   
        ↓  
140.82.114.4  
Then it establishes the network connection.  

***What is nslookup?***
nslookup (Name Server Lookup) is a command-line tool used to query DNS (Domain Name System) servers.  
It helps you find:  
•	The IP address of a domain name   
•	The hostname for an IP address (reverse lookup)   
•	DNS records (MX, NS, TXT, etc., depending on the implementation)   
•	Whether a DNS server is working correctly   
It is one of the most common tools for troubleshooting DNS and name resolution.  
``nslookup [domain]``  
```nslookup [IP-address]```  

**Common DNS Record Types**  
Record	Purpose  
A	Hostname → IPv4 address  
AAAA	Hostname → IPv6 address  
MX	Mail server  
NS	Name server  
TXT	Text information (SPF, DKIM, verification)  
PTR	Reverse DNS (IP → hostname)  
CNAME	Alias to another hostname  
DNS (Domain Name System)  
DNS uses both UDP and TCP on port 53.   
DNS over UDP  
•	UDP is the default protocol for most DNS queries.     
•	It is faster because it is connectionless and has less overhead.    
•	It is used for standard hostname-to-IP lookups.  

**Netplan** is a network configuration utility used in modern Ubuntu systems (starting with Ubuntu 17.10) to configure network interfaces.  
Instead of editing configuration files directly, you define your network settings in YAML files under:  
```/etc/netplan/```   
Netplan then generates the appropriate configuration for the underlying network service, such as:  
•	systemd-networkd   
•	NetworkManager  
**Why Use Netplan?**  
Netplan makes network configuration:  
•	Easier to read (YAML format)   
•	Consistent across systems   
•	Suitable for servers and desktops   
•	Easy to automate   
It can configure:  
•	Static IP addresses     
•	DHCP   
•	DNS servers   
•	Default gateways   
•	VLANs   
•	Bridges   
•	Bonds   
•	Routes  

``sudo netplan apply``  
```sudo netplan try```
View the configuration:  
``cat /etc/netplan/*.yaml``  
Netplan YAML Structure  
network:
  version: 2
  renderer: networkd

  ethernets:
    eth0:
      dhcp4: false

      addresses:
        - 192.168.1.100/24

      routes:
        - to: default
          via: 192.168.1.1

      nameservers:
        addresses:
          - 8.8.8.8
          - 1.1.1.1




A ***firewall*** is a network security system that monitors and controls incoming and outgoing network traffic based on predefined security rules.  
Its main purpose is to allow authorized traffic and block unauthorized or malicious traffic.  
Think of a firewall as a security guard at the entrance of a building:  
•	✅ Allows authorized people to enter.   
•	❌ Blocks unauthorized people.   
Similarly, a firewall decides whether network packets are allowed to pass.  
Stateful vs Stateless Firewall  
A firewall can inspect traffic in two different ways:  
1.	Stateless Firewall   
2.	Stateful Firewall   
The main difference is:  
•	Stateless firewall examines each packet independently.   
•	Stateful firewall remembers active network connections and makes decisions   based on the connection's state.   
**Stateless Firewall**  
A stateless firewall treats every packet as a completely new packet.  
It does not remember previous packets or whether a connection already exists.  
It only checks:  
•	Source IP    
•	Destination IP   
•	Source Port   
•	Destination Port   
•	Protocol (TCP/UDP/ICMP)   
Then it decides whether to allow or deny the packet.  
**Stateful Firewall** 
A stateful firewall remembers active connections.     
It keeps a state table (also called a connection table).    
When a new connection starts:    

***What is iptables?***  
iptables is a Linux firewall utility used to configure the Linux kernel's Netfilter firewall.  
It allows you to:  
•	Allow or block network traffic   
•	Filter packets based on IP address, port, or protocol   
•	Perform NAT (Network Address Translation)   
•	Log network traffic   
•	Protect servers from unauthorized access   
Although nftables is the modern replacement, iptables is still widely used and is a common interview topic.  
Netfilter and iptables  
•	Netfilter → The firewall framework built into the Linux kernel.   
•	iptables → The command-line tool used to configure Netfilter.   
iptables Command  
       │  
       ▼  
Netfilter (Kernel)  
       │  
       ▼  
Allow / Block Packets  


**Chains**  
Each table contains chains, which are groups of rules.  
Chain	Description  
INPUT	Traffic coming into the local machine  
OUTPUT	Traffic leaving the local machine  
FORWARD	Traffic passing through the machine (router/firewall)   
**What is firewalld?**  
firewalld (Firewall Daemon) is a dynamic firewall management service for Linux.  
It provides an easier way to manage firewall rules than using iptables directly.  
firewalld is the default firewall on many Red Hat-based distributions:    
•	RHEL   
•	Rocky Linux   
•	AlmaLinux   
•	CentOS   
•	Fedora   
Internally, modern versions of firewalld use nftables (older versions used iptables).  
UFW (Uncomplicated Firewall) is a simple firewall management tool for Linux.  
It is designed to make firewall configuration easier than using iptables directly.  
UFW is the default firewall tool on Ubuntu.  
**Internally:**  
You use simple ufw commands, and UFW creates the necessary firewall rules behind the scenes.  
How iptables Works (Simple Explanation)  
Example Commands  
Allow SSH:  
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT  
Meaning:  
•	-A INPUT → Add a rule to incoming traffic.   
•	-p tcp → Match TCP packets.   
•	--dport 22 → Match destination port 22.   
•	-j ACCEPT → Allow the packet.  
Block Telnet:  
sudo iptables -A INPUT -p tcp --dport 23 -j DROP  
Meaning:  
•	If someone tries to connect to port 23, discard the packet.   
Insert a Rule (-I = Insert)  
Insert the rule at the top of the chain:  
sudo iptables -I INPUT 1 -p tcp --dport 22 -j ACCEPT  
Delete a Rule (-D)  
Delete rule number 3 from the INPUT chain:  
sudo iptables -D INPUT 3  
Or delete by specifying the full rule:  
sudo iptables -D INPUT -p tcp --dport 22 -j ACCEPT  
Replace a Rule (-R)  
Replace rule number 2:  
sudo iptables -R INPUT 2 -p tcp --dport 443 -j ACCEPT  
Flush a Chain (-F)  
Remove all rules from all chains:  
sudo iptables -F  
Flush only the INPUT chain:  
sudo iptables -F INPUT  
Set the Default Policy (-P)  
Block all incoming traffic by default:  
sudo iptables -P INPUT DROP  
Allow all outgoing traffic:  
sudo iptables -P OUTPUT ACCEPT  
Interview Tip  
The three options that interviewers ask about most often are:  
•	-A → Append a rule to the end of a chain.   
•	-I → Insert a rule at a specific position (often the top).   
•	-D → Delete a rule.  
ARP (Address Resolution Protocol) is a networking protocol used to map an IPv4 address   to a device's MAC (Media Access Control) address on a local area network (LAN).   
Example 
IP Address	MAC Address  
192.168.1.10	00:1A:2B:3C:4D:5E  
192.168.1.20	A4:B1:C2:D3:E4:F5  
Arp -a  
netstat (Network Statistics) is a command-line tool used to display information about  network connections, routing tables, network interfaces, and listening ports.  
It is one of the most common tools for troubleshooting network problems on Linux and Windows.  
Show all active connections  
netstat  
Example output:  
Proto Recv-Q Send-Q Local Address      Foreign Address    State  
tcp        0      0 192.168.1.10:22    192.168.1.5:52341  ESTABLISHED   

























