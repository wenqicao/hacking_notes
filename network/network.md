# NETWORK

* [Spoofr](https://github.com/d4rkcat/Spoofr) - ARP poison and sniff with DNS spoofing, urlsnarf, driftnet, ferret, dsniff, sslstrip and tcpdump  
* [ProxyChains](http://proxychains.sourceforge.net/) - TCP and DNS through proxy server. HTTP and SOCKS
* arpspoof
* [Ettercap](http://ettercap.github.io/ettercap/) - suite for man in the middle attacks
* netdiscover
* [Yersinia](http://www.yersinia.net/) - network tool designed to take advantage of weaknesses in different network protocols
* [iodine](https://github.com/yarrick/iodine) - tunnel IPv4 data through a DNS server
* [dnscat2](https://github.com/iagox86/dnscat2) - encrypted C&C over DNS

Discovery
---------
`netdiscover`  

DNS Cache Snooping
------------------

`nmap -sU -p 53 --script dns-cache-snoop.nse 8.8.8.8`

Wireshark
---------

Filters:
```
tcp.port==25
tcp.srcport!=53
tcp.dstport==80
ip.addr == 10.0.0.1
ip.addr != 10.0.0.1
ip.src==192.168.0.0/16
!udp
smb || dns || icmp
```

NMAP
----

`-iR` use random IP addresses  
`-iL` scan form file  
`-sT` connect scan (3-way handshake)  
`-sS` stealth scan (SYN)  
`-sA` ACK method  
`-vv` increased verbosity  
Spoof MAC: `--spoof-mac Cisco`  
Bad checksum: `--badsum`  
Source port spoof: `--source-port 53`  

* Output:  
`-oN` same as on screen  
`-oG` greppable format  
`-oX` XML format  
`-oA` all formats  

* While scanning:  
`p` packet tracing  
`v` verbosity  

TCP/IP
======

OSI Model
---------

1. Physical (cables, hubs); PDU: bit
2. Data Link (frames); PDU: frame
3. Network (packets); PDU: packet
4. Transport (TCP); PDU: segment (TCP), datagram (UDP)
5. Session (logical ports); PDU (5-7 layers): data (clear text, encrypted, compressed)
6. Presentation (ASCII)
7. Application (SMTP)

TCP Flags
---------

* CWR – Congestion Window Reduced (CWR) flag is set by the sending host to indicate that it received a TCP segment with the ECE flag set (added to header by RFC 3168).
* ECE (ECN-Echo) – indicate that the TCP peer is ECN capable during 3-way handshake (added to header by RFC 3168).
* URG – indicates that the URGent pointer field is significant
* ACK – indicates that the ACKnowledgment field is significant (Sometimes abbreviated by tcpdump as ".")
* PSH – Push function
* RST – Reset the connection (Seen on rejected connections)
* SYN – Synchronize sequence numbers (Seen on new connections)
* FIN – No more data from sender (Seen after a connection is closed)

Other
=====

* MAC address spoof: `ifconfig eth0 hw ether 00:11:22:33:44:55`  
* ARP spoof:
```
arpspoof -i eth0 192.168.0.1
arpspoof -t 10.0.0.1 10.0.0.2
arpspoof -t 10.0.0.2 10.0.0.1
```  
* View routing tables: `netstat -rn`  
