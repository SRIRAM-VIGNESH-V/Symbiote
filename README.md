#  Project Symbiote

Invisible protocol sniffer for finding vulnerabilities in the network and a network hardening tool based on Scapy.

Author: SRIRAM VIGNESH V



# Mechanics

Symbiote is a invisible network sniffer for finding vulnerabilities in network equipment. It is based entirely on network traffic analysis, so it does not make any noise on the air. Symbiote is completely invisible. Purely based on the Scapy library.

Symbiote allows pentesters to automate the process of finding vulnerabilities in network hardware. Discovery protocols, dynamic routing, FHRP, STP, LLMNR/NBT-NS, etc.

## Supported protocols

Detects up to 22 protocols:

```
MACSec
EAPOL
ARP (Passive ARP)
CDP (Cisco Discovery Protocol)
DTP (Dynamic Trunking Protocol)
LLDP (Link Layer Discovery Protocol) 
802.1Q Tags (VLAN)
STP (Spanning Tree Protocol)
OSPF (Open Shortest Path First)
EIGRP (Enhanced Interior Gateway Routing Protocol)
VRRP (Virtual Router Redundancy Protocol)
HSRP (Host Standby Redundancy Protocol)
GLBP (Gateway Load Balancing Protocol)
IGMP (Internet Group Management Protocol)
LLMNR (Link Local Multicast Name Resolution)
NBT-NS (NetBIOS Name Service)
MDNS (Multicast DNS)
DHCP (Dynamic Host Configuration Protocol)
DHCPv6 (Dynamic Host Configuration Protocol v6)
ICMPv6 (Internet Control Message Protocol v6)
SSDP (Simple Service Discovery Protocol)
MNDP (MikroTik Neighbor Discovery Protocol)
```
## Operating Mechanism

Symbiote works in two modes:

- Hot mode: Sniffing on your interface specifying a timer
- Cold mode: Analyzing traffic dumps

The tool is very simple in its operation and is driven by arguments:

- Interface: Specifying the network interface on which sniffing will be performed
- Timer: Time during which traffic analysis will be performed
- Output pcap: Symbiote will record the listened traffic to `.pcap` file, its name you specify yourself
- Input pcap: The tool takes an already prepared `.pcap` as input and looks for protocols in it
- Passive ARP: Detecting hosts in a segment using Passive ARP

```
usage: Symbiote.py [-h] [--interface INTERFACE] [--timer TIMER] [--output-pcap OUTPUT_PCAP] [--input-pcap INPUT_PCAP] [--passive-arp]

options:
  -h, --help            show this help message and exit
  --interface INTERFACE
                        Interface to capture packets on
  --timer TIMER         Time in seconds to capture packets
  --output-pcap OUTPUT_PCAP
                        Output filename for pcap file
  --input-pcap INPUT_PCAP
                        Path to the input PCAP file for analysis
  --passive-arp         Host discovery (Passive ARP)
```

---

## Information about protocols

The information obtained will be useful not only to the attacker, but also to the security engineer, he will know what he needs to pay attention to.

When Symbiote detects a protocol, it outputs the necessary information to indicate the attack vector or security issue:

- Impact: What kind of attack can be performed on this protocol;

- Tools: What tool can be used to launch an attack;

- Technical information: Required information for the attacker, sender IP addresses, FHRP group IDs, OSPF/EIGRP domains, etc.

- Mitigation: Recommendations for fixing the security problems

---




# How to Use

```

Symbiote requires at least an interface and a timer at startup. Choose the timer from your calculations.

> To stop traffic sniffing, press CTRL + С

If you need to record the sniffed traffic, use the `--output-pcap` argument

> By specifying only the --interface and --output-pcap - Symbiote will also be able to start, without a timer

If you already have some recorded traffic, you can use the `--input-pcap` argument to look for potential security issues

# Passive ARP

The tool can detect hosts without noise in the air by processing ARP frames in passive mode


[+] Host discovery using Passive ARP

┌─────────────────────────────────────┐
│            Detected Host            │
├─────────────────────────────────────┤
│ Host IP Address: 192.168.0.251      │
│ Host MAC Address: 02:10:de:64:f2:32 │
└─────────────────────────────────────┘
┌─────────────────────────────────────┐
│            Detected Host            │
├─────────────────────────────────────┤
│ Host IP Address: 192.168.0.213      │
│ Host MAC Address: 00:0c:27:7f:2b:c6 │
└─────────────────────────────────────┘


