# Networked Systems Notes
## Lecture 1
### Slides

**Networked System** : A cooperating set of autonomous computing devices that exchange data to perform some application goal 

_Applications goals_
- **Communication** : how is information exchanged across a single link? 
- **Networking** : how are links connected to form a wide area network?
- **Internetworking** : how are networks interconnected to from an internet? How is data routed across that network? 
- **Transport** : how do end-systems reliably exchange data?

**Communication Protocols**
- Channel constraints bound communications speed and reliability
- The message syntax, semantics, and communication patterns form a network protocol – HTTP, TCP, IP, etc.
- Protocols can be composed and layered to raise level of abstraction

**Network Protocols** : Formal standards and policies made up of rules, procedures and formats that defines communication between two or more devices over a network

**Protocol Layering: The OSI Reference Model**

Application <\-\-\-\> Application

Presentation <\-\-\-\> Presentation

Session <\-\-\-\> Session

Network <\-\-\-\> Network \- Network <\-\-\-\> Network

Data Link <\-\-\-\> Data Link \- Data Link <\-\-\-\> Data Link

Physical 

End System \-\-\- Router \-\-\- End System

- A standard model of layered protocol design – real networks don’t follow this model – they’re more complex, and layer violations, sublayers, and tunnels are commonplace 
- A layered model is extremely useful for helping structure discussions about networks

**The Physical Layer**
Physical layer enables communication \- transmission of raw bitstream 
- What type of cable or wireless link do you use? 
- How to encode bits onto that channel? Baseband encoding, Carrier modulation etc.
- What is the capacity of the channel?

**Baseband encoding** : encodes a stream of bits into a dedicated channel, allowing successful transmission of data

**Carrier modulation** : the process of imposing an input signal onto a carrier wave is called modulation. In other words, modulation changes the shape of a carrier wave to somehow encode the speech or data information that we were interested in carrying

_Carrier wave_ : a waveform \(usually sinusoidal\) that is modulated \(modified\) with an information\-bearing signal for the purpose of conveying information

_Sinusoidal_ : having the form of a sine curve

**Encoding Data onto Wired Channels**

- Signal usually directly encoded onto the channel, by varying some property of the channel, and occupies baseband region
- The maximum bitrate of a channel is described by Nyquist’s theorem: R<sub>max</sub> &le; 2Blog<sub>2</sub>V
- _B_: bandwidth of the channel
- _V_ : number of discrete values per symbol
- Maximum data rate only reached with a noise\-free channel

**Baseband Data Encoding**

_Non-return to zero (NRZ) encoding_ : 
- Encode a 1 as a high signal, 0 as low signal 
- No variation in waveform if long runs of same value sent \- easy to miscount number of bits

_Manchester encoding:_
- Encode a 1 as high-low transition, a 0 as a low\-high transition 
- Doubles bandwidth needed, since transition on every bit, but avoids miscount

Signal encoded onto the channel by varying channel characteristics – voltage applied to an electrical cable, intensity of laser in optical fibre

**Encoding Data onto Wireless Channels** 

_Shifts signal from baseband to a higher carrier frequency_

- Carrier wave applied to channel at frequency, C; signal modulated onto the carrier
- Bandwidth unchanged, but shifted to range centred on the carrier frequency
- Wireless links use carrier modulation, rather than baseband transmission 
- Allows multiple signals on a channel, modulated onto carriers of different frequency
- Performance affected by carrier frequency, transmission power, modulation scheme, type of antenna, etc.

**Amplitude, Frequency, Phase Modulation**

Complex modulations are possible: Gigabit Ethernet uses amplitude modulation with five different amplitudes

Modulation schemes are often combined: for example, dial\-up modems vary phase and amplitude \-\> quadrature amplitude modulation with 12 phase shift values at two different amplitudes

_Modem_ : a hardware device that converts data from a digital format

_Refer to 01c for a diagram showing visual representations of modulation_

**Spread Spectrum Communication**
- Single frequency channels prone to interference 
- Mitigate by repeatedly changing carrier frequency, many times per second: noise unlikely to affect all frequencies 
- Use a pseudo\-random sequence to choose which carrier frequency is used for each time slot 
- Seed of pseudo-random number generator is shared secret between sender and receiver, ensuring security

_Example: 802.11b Wi-Fi uses spread spectrum using several frequencies centred at either 2.4 GHz or 5 GHz_

_Spread spectrum_ : Changing the carrier frequency several times per second to avoid obstacles at a particular range

**Physical Link Characteristics and Limitations**

- Real-world network links are imperfect, and subject to noise

_noise_ : Electrical or radio interference, imperfections in optical fibre

- The Shannon-Hartley theorem predicts the maximum data rate of a channel subject to noise: R<sub>max</sub> = Blog<sub>2</sub>\(1 + s/n\)
- _B_ : bandwidth of the channel 
- _S_ : signal strength
- _N_ : noise strength
- Assuming Gaussian noise: interference affects all frequencies equally

_Physical limit on maximum transmission rate_
- B and N depend on properties of the channel
- S depends on transmission power \-\> trade battery life for performance

**The Data Link Layer**

- Physical layer enables communication 
- Data link layer provides framing, addressing, media access control 
- Structure the bitstream into meaningful frames of data 
- Detect and correct transmission errors 
- Identify devices
- Arbitrate access to the channel

**Framing and Addressing**

Separate the bitstream into meaningful frames of data

_Refer to 01c for an example ethernet frame format_

Preamble \-\- Source Address \-\- Destination Address \-\- Len \-\- Data \-\- CRC

_CRC_ : Cycle Redundancy Check, error-detecting code commonly used in digital networks and storage devices to detect accidental changes to raw data

**Media Access Control** : Control when frames are sent, to avoid collisions

_Examples: Ethernet, Wi\-Fi_

- When propagation delay low, listen before sending
- If link is idle, send data immediately
- If another transmission is active, or if collision occurs, stop sending, wait, then retransmit 

- Wait time should be random – to avoid deterministic repeated collisions; pick a random initial back-off interval of x seconds ± 50%
- Wait time should increase with number of collisions – repeated collisions signal congestion; reduce transmission rate allows network to recover; each repeated collision before success, x \-\> 2x

_Improves utilisation_
- Active transmissions not disrupted by collisions
- Only the new sender backs-off if the channel is active

_Why does propagation delay matter?_

A \-\-\> <\-\- B

- A starts transmitting
- B listens, hears no traffic \(message from A hasn’t reached it yet\)
- B starts transmitting

_Collision occurs, as messages overlap in transit; smaller propagation delay \-\> less likely to occur_

**The Network Layer as an Internet Protocol**

- Global inter-networking protocol 

**Hour glass protocol stack**

**Application Presentation** : MIME, HTML, SDP, Codecs

**Session** : SMTP, HTTP, SIP, RTP

**Transport** : TCP, UDP

**Network** : IP

**Data Link** : Ethernet, ADSL, Wi\-Fi, SONET

**Physical** : Wireless, Twisted pair, Optical Fibre

**IP** : Single standard network layer protocol
- Packet switched network, best effort service 
- Uniform network and host addressing 
- Uniform end-to-end connectivity \- subject to firewall policy

- Many transport & application layer protocols 
- Range of link-layer technologies supported 
- Decouples end-to-end functionality from per-hop functionality

**End\-to\-end functionality**: when an application performs specific tasks from start to finish,

**Per-hop functionality** : a network solution aimed at classifying the IP traffic flow into traffic classes. It uses six bits, called DiffServ Code Point 

_DiffServ_ : a computer networking architecture that specifies a simple and scalable mechanism for classifying and managing network traffic

**IPv4**
- 32 bit addresses insufficient
- Fragmentation difficult at high data rates
- Limited extensibility

**IPv6**
- Larger address space
- No in-network fragmentation
- No unnecessary checksum 
- Simpler header format

_fragmentation_ : process that breaks packets into smaller pieces (fragments), so that the resulting pieces can pass through a link with a smaller maximum transmission unit (MTU) than the original packet size

_checksum_ : a small-sized block of data derived from another block of digital data for the purpose of detecting errors that may have been introduced during its transmission or storage

**What About IPv5?**
- Experiments with voice over the ARPAnet \- the precursor to the Internet \- started in the early 1970s
- **Network Voice Protocol** : network protocol for transporting human speech over packetized communications networks
- This evolved into the Internet Stream Protocol, ST-II, that was assigned IPv5 – an experimental multimedia streaming protocol developed between 1979 and 1995, but never widely deployed
- **ST-II+ specification** : distinguishes its own packets with an Internet Protocol version number 5, uses the same IP address structure and the same link layer protocol number as IP

**IP Addressing**
- IP addresses encode location of network interface
- If a host has multiple network interfaces \(e.g., Wi-Fi and Ethernet\), it will have multiple IP addresses
- A host can support both IPv4 and IPv6 on each interface
- A host can have multiple IP addresses of each type assigned to each interface

_DNS names are an application concept \- not used by the network_

_Domain Name System_ :  translates human readable domain names \(for example, www.amazon.com \) to machine readable IP addresses \(for example, 192.0. 2.44\).

**Routing**
- Each network administered separately - an autonomous system \(AS\)
- Different technologies
- Different policies
- Mutual distrust \- between AS and its peers; between AS and its customers

**Autonomous Systems and Inter-domain Routing**
- Separately administered; different technologies
- Shortest path routing
- Distance vector or link state algorithms

**Inter-domain Routing and BGP**
- Treats each network as a graph node and routes between ASes 

_The AS-level topology:_
- Well connected core; sparse edges 
- Edge networks can use default route to the core
- Core networks need full routing table: the default free zone \(DFZ\) 

_Routing between competitors \- no real trust between organisations_
- Policy, politics, and economics are key constraints; not shortest path
- **BGP routing protocol** : a standardized exterior gateway protocol designed to exchange routing and reachability information between autonomous systems on the Internet

**Forwarding**
- Best effort, connectionless, packet delivery 
- Just send \- no need to setup a connection first
- Network makes its best effort to deliver packets, but provides no guarantees 
- Time taken to transit the network may vary 
- Packets may be lost, delayed, reordered, duplicated or corrupted 
- The network discards packets it can’t deliver 
- Easily run over any type of link layer

**TCP and UDP Transport**

- IP network provides best effort service 
- Packets can be lost, duplicated, delayed, or re-ordered

_Transport isolates applications from the network_
- Demultiplexes traffic for different applications
- Enhances network quality of service to offer appropriate reliability 
- Performs congestion control, adapts to network capacity

_Only two deployable transport protocols in the Internet:_
- **UDP** : user datagram protocol
- **TCP** : transmission control protocol

**UDP**

- Simplest transport protocol

_Exposes raw IP service to applications_
- Connectionless, best effort packet delivery: framed, but unreliable
- No congestion control
- Adds 16 bit port number to identify services

_Used by applications preferring timeliness over reliability_
- Voice-over-IP
- Streaming video
- Gaming 

- Must be able to tolerate some loss of data
- Must be able to adapt to congestion in the application layer

_Refer to 01e for UDP diagram_

**TCP**

_Reliable, ordered, byte stream delivery service running over IP_
- Lost packets are retransmitted; ordering is preserved; message boundaries are not preserved 
- Adapts sending rate to match network capacity \-\> congestion control
- Adds port number to identify services 

Used by applications needing reliability \-\> default choice for most applications

_Refer to 01e for TCP diagram and format layout_

**TCP Congestion Control** : Converge on fair share of path capacity using AIMD algorithm

_AIMD_ : additive-increase/multiplicative-decrease algorithm is a feedback control algorithm best known for its use in TCP congestion control. AIMD combines linear growth of the congestion window with an exponential reduction when congestion is detected

**Higher Layer Protocols**

_The OSI reference model defines three layers above the transport:_
- Session layer 
- Presentation layer 
- Application layer 

- Internet architecture makes no clear distinction between these layers

_Goal \- support application needs:_
- Manage transport layer connections
- Name and locate application-level resources 
- Negotiate data formats, and perform format conversion if needed 
- Present data in appropriate manner 
- Implement application-level semantics

**Session Layer: Managing Connections**
- What connections does the application need?
- How to find participants?
- How to setup connections? 
 

_How does session membership change?_
- Does the group size vary greatly?
- How rapidly do participants join and leave?  
- Are participants aware of other members?

_Refer to 01f for diagrams of example application connections_

**The Presentation Layer**

_Managing the presentation, representation, and conversion of data:_
- Media types and content negotiation 
- Channel encodings 
- Internationalisation, languages, and character sets

Common services used by many applications. 

**The Application Layer**

_Protocol functions specific to the application logic_
- Deliver email 
- Retrieve a web page
- Stream video 

**Protocol Standards**

- The OSI model is a reasonable way of thinking about network protocols

_But – it misses two key layers:_
- Financial
- Political 

- Successful network protocols support interoperability between different vendors \- this interoperability exists because those vendors work to standardise the protocols

**Rough consensus and running code** : standards are the result of much discussion and negotiation

**The Changing Internet: Architectural Assumptions**

_The original design of the Internet made certain assumptions:_
- Devices are generally located in a fixed location, and have a small number of network interfaces that are uniquely addressable 
- The network and services are decentralised 
- Best effort service provides sufficient quality
- The network is trusted
- Innovation can happen at the edges; the network is dumb 

Reasonable for the 1980s, when the IP architecture was defined, but the network has changed \- how have the protocols changed?

**Changes in Addressing and Reachability**

_Assumption: every network interface has unique IP address_
- Devices uniquely addressable with uniform connectivity
- In principle, any device can connect to any other; policy enforced by firewalls, privacy protected by changing address assignments 

- IPv4 has insufficient addresses to support this model 
- IPv6 deployment is slow; NAT is widespread

_Implication: connectivity becomes difficult_
- Dual-stack IPv4/IPv6 connection racing \(“happy eyeballs”\)
- NAT traversal for peer-to-peer applications
- Complicates software design and implementation
- Forces reliance on cloud services and encourages centralisation

**IPv4 Address Exhaustion**

- IANA assigned last IPv4 block to regional Internet registries \(RIRs\) in 2011 
- RIRs have exhausted the available IPv4 addresses, or soon will

_IANA_ : The Internet Assigned Numbers Authority is a standards organization that oversees global IP address allocation

_IPv6 Deployment is Slow_

**Establishing Connectivity in the Modern Internet**

_NAT traversal \-\> binding discovery, exchange, probing_
- STUN, TURN, and the ICE algorithm
- Requires a server with public IP address forbinding discovery; centralised point of control
- Complex, slow, unreliable, wastes power, generates unnecessary traffic

_NAT_ : Network address translation is a method of remapping an IP address space into another by modifying network address information in the IP header

_Dual stack \-\> connection racing_
- Some paths support IPv4, some IPv6; probingand connection timeouts slow for client-serverapplications
- Race connections by probing in parallel: hardto implement, wastes resources 

NAT and dual stack operation complicates connection establishment; encourages centralisation onto cloud services.

**Increasing Mobility**

- IP addresses intended to encode location in the network 

_**Ubiquitous mobile devices** \- smartphones \- complicate addressing and reachability since devices change their IP address each time they move:_
- TCP connections must be re-established after each move 
- UDP packets must be redirected after each move
- Complex signalling and connection management if devices move frequently

**Hypergiants and Centralisation**

- Internet topology is flattening, becoming increasingly centralised 
- Transit network ecosystem being replaced by direct connections from “eyeball” networks to content providers – Google, Facebook, Amazon, Akamai, ...  
- Implications for network neutrality, competition, innovation

_Refer to 01g for a diagram further explaining this concept_

**Supporting Real-time Traffic**

_Video streaming dominates Internet traffic, growing \>40% per year_
- Packet loss \-\> quality impairments or increased delay
- Driving centralisation and direct CDN connections \-\> easier to manage quality
- Driving TCP congestion control and TCP replacements \-\> BBR algorithm, QUIC; low-latency 

_Interactive real-time media has stricter constraints_
- WebRTC, Zoom, VoIP, gaming, ... \-\> non-TCP transport to lower latency

**Supporting Real-time Traffic: Impact of COVID-19**
- Residential networks saw \>20% increase in traffic overnight at the start of the COVID-19 lockdown
- Mobile networks saw \~10% drop in traffic

- Video conferencing providers saw massive growth in traffic
- The Internet was flexible enough to support this shift – can we maintain such flexibility while also improving quality?

_Refer to 01g for web traffic stats during COVID\-19 pandemic_

**Innovation in the Network**

_Can we still change the network protocols?_
- NATs, firewalls, middleboxes \-\> TCP is hard to change now
- Transport encryption, tunnel over UDP \-\> QUIC? Pervasive encryption to defeat pervasive monitoring and surveillance? 
- Protocol ossification is a real concern
- Is the model smart edges and a dumb network appropriate? 

_Can new startups compete with the hypergiants?_
- Several forces pushing towards centralisation \- can we evolve the network to counter these? 
- Can we enable a decentralised network?

**Can the network evolve to address these challenges?**
- How to establish connections in a fragmented network? 
- How can encryption protect against pervasive monitoring and prevent transport ossification?
- How can we reduce latency and support real\-time and interactive content? 
- How can we adapt to the vagaries of wireless networks? 
- How can we identify and distribute content? How can we manage the tussle for control of the DNS and naming? 
- How can we manage interdomain routing to efficiently delivery content?
- How can we re-decentralise the network?

### Videos

**Optical Fibre** : modulation by intensity of light

**Electrical Wire** : modulation by voltage

Modulation directly corresponds to the signal to be sent

**Bandwidth** : The range of frequencies occupied by a signal

_Twisted pair maximum bandwidth depends on the length of the wire, the tightness of twists and the thickness of the wires_

IN NRZ, in long runs of the same value it can be difficult to determine exactly how long that value has been sent leading to miscounting

Amplitude modulation is more susceptible to noise than frequency modulation

Real systems use multiple types of modulation

**Preamble** : pattern that can only occur at the start of a message

**Header** : Gives information such as addresses and the length of a message

_Start code assists in synchronisation and timing recovery_

Collisions are more likely to occure in large networks with propagation delays but can happen in any network

_CSMA/CD can double the wait time each time a collision occurs and resets the wait time when a successful transmission occurs_

The network layer provides flexibility but is not optimised for performance

_Uniform network_ : anyone can send anyone else signals subject to firewall policies

IPv4 allows for fragmentation of large packets over smaller bandwidth networks.

**DSCP** : allows for a packet to be considered higher priority in a network

IPv6 requires a host to adjust packet size themselves to adapt to a network as it does not allow for fragmentation.

_An IP address identifies the location where a device accesses a network not the device itself._

**BGP** : Border Gateway Protocal, allows for each AS to advertise the network prefixes it owns to tell the rest of the network where to send packets destined for IP addresses within those prefixes

_Channel encodings_ : adapting data to fit the limitations of the channel

## Week 2
### Slides

#### TCP Connections

- Typical TCP\-based applications are client\-server 
- Server listens for connections on a well\-known port 
- Clients connects to the server 
- Client sends requests; server responds 

- Can be used in a peer\-to\-peer manner 
- The two peers simultaneously connect\(\) to each other, then send and receiver data 
- Uncommon, but possible – requires both peers to have known and accessible IP addresses, and to bind\(\) to known ports

#### TCP Client\-Server Connection Establishment 

- The server calls accept\(\) and waits 

_The connect() call triggers the three-way handshake:_

**Client → Server:**
- SYN \(“synchronise”\) bit set in TCP header 
- Client’s initial sequence number chosen at random 

**Server → Client:**
- SYN 
- ACK for client’s initial sequence number 
- Server’s initial sequence number chosen at random 

**Client → Server:**
- ACK for server’s initial sequence number 

- When handshake completes, connection is established

- Calls send\(\)/recv\(\) transmit data 
- For short flows, initial three\-way handshake can take a significant fraction of connection lifetime

#### Impact of Latency on Performance 

_Assume a very simple web page:_
- 1x HTML file, 1x CSS file, and 1x image 
- HTML and CSS files hosted on one server, image on a different server 
- Everything retrieved via HTTP over TCP/IP 

_How long does it take to retrieve that page?_
- 1x RTT handshake to connect to server 1 
- 1x RTT + serialisation time to fetch HTML file 

\+ Longest of:
- 1x RTT \+ serialisation time to fetch CSS file 

and:

- 1x RTT handshake to connect to server 2 
- 1x RTT + serialisation time to fetch image

- Performance depends on RTT and available bandwidth 

_What is a typical RTT?:_
- Depends on distance 
- Depends on network congestion 

_What is typical available bandwidth?:_
- ADSL2\+ → 25Mbps 
- VDSL → 50Mbps 
- 4G wireless → 15-30Mbps 

**all assuming otherwise idle network**

_Latency hurts performance_
- Connection establishment is slower 
- Retrieving data takes longer

_As RTT increases, benefits of increasing   bandwidth reduce:_
- For this example, with 300ms RTT, increasing   bandwidth from 15Mbps to 1Gbps gives only  22% reduction in page download time 
- Connection setup time – the 3\-way handshake   of TCP – dominates in many scenarios 

**Refer to slides 02A for examples in different transfer protocols for fetching data**

#### Impact of Transport Layer Security 

_The protocol running over TCP can also impact performance:_
- HTTP sends and retrieves data immediately the TCP connection is open 
- HTTPS opens a TCP connection, negotiates security parameters using TLS within that TCP connection, then starts to send and receive encrypted data – what impact does this have?

_Revisit simple web page download example:_
- 1x HTML file, 1x CSS file, and 1x image 
- HTML and CSS files hosted on one server, image on a different server 
- Everything retrieved via HTTPS over TCP/IP 

_TLS v1.3 introduces two RTTs extra latency:_
- One extra RTT per connection to negotiate security parameters 
- Further causes impact of RTT and connection establishment to dominate performance

#### Impact of Latency on TCP Performance 

_For client\-server applications, each request takes 1x RTT plus data serialisation time:_
- Unless data is very large, RTT is often most significant performance factor 
- Each TCP connection has 1x RTT connection setup overhead 
- If TLS v1.3 is used inside TCP, an additional 1x RTT 
- If TLS v1.2 is used inside TCP, an additional 2x RTT 

_To improve performance in your application:_
- Reduce the number of TCP connections used 
- Limit the number of request-response exchanges between client and server

#### Impact of IPv6 and Dual Stack Deployments

_IPv4 → IPv6 transition means we have two Internets:_
- Some hosts only connect via IPv4, some only via IPv6, some have both types of address 
- Some links carry only IPv4 traffic, some only IPv6 traffic, some both types of traffic 
- Some firewalls block IPv4, some block IPv6, some block both types of traffic 

- IPv6 network is not a subset of the IPv4 network; it’s separate, but overlaps in places

#### Happy Eyeballs 

_How to connect to a host with more than one IP address?_
- Perform DNS lookups for IPv4 and IPv6 in parallel; start with whichever completes first 
- Call connect\(\) for that address; if not connected within \~100ms, start connect\(\) to next address on the list in parallel, alternating between IPv4 and IPv6
- Use first connect\(\) that succeeds, drop other successful connections 
- Balances speed to connect vs network overload by trying all at once in parallel

#### Peer\-to\-peer Connection Establishment 

- The Internet is conceptually a peer\-to\-peer network – any device can, in principle, talk to any other 
- You should be able to run a TCP server on any device 
- You should be able to run a TCP\- or UDP\-based peer\-to\-peer application 
- In practise peer-to-peer connection establishment is difficult, due to network address translation \(NAT\)

#### Network Address Translation \(NAT\) 

- IPv4 address space is exhausted 
- IPv6 is the long\-term solution, but the transition is taking many years
-  Network address translation \(NAT\) is a workaround for the shortage of IPv4 addresses; it allowing several devices to share a single IP address

#### Connecting a Single Host

- An Internet service provider (ISP) owns an IP address prefix
- They assign a customer a single address for a single host

- An Internet service provider owns an IP address prefix
- They assign a customer a single address for a single host 
- No address translation

#### Connecting Multiple Hosts

- The customer buys another host 
- How does it connect?

_What’s supposed to occur:_
- Customer acquires a router, which gets the customer’s previous IP address 
- ISP assigns new range of IP addresses to customer \(from the ISP’s prefix\) 
- Customer gives each host an address from that new range
- No address translation

#### Network Address Translation 

_What actually happens:_
- Customer acquires a NAT router, which gets the customer’s previous IP address 
- Customer gives each host on their network a private address

_NAT performs address translation on packets traversing it:_
- Change source IP address in packet header to match external address of NAT 
- Change source TCP/UDP port in packet header to some unused value 
- Records the mapping, so the reverse changes can be made to any incoming replies as they traverse the NAT in the reverse direction

#### NAT and Private Address Ranges 

- The NAT hides a private network behind a single public IP address 
- The private IP network address ranges are 10.0.0.0/8, 176.16.0.0/12, and 192.168.0.0/16 

- Gives the illusion of more address space, by reusing IP addresses in different parts of the network 

#### NAT Routers Encourage Centralisation

- Client\-server applications with client behind NAT work without changes – web and email 
- Client-server applications with server behind NAT fail – need explicit port forwarding 
- Peer\-to\-peer applications fail – complex NAT traversal algorithm needed to connect 
- Encourages centralisation of services

#### NAT Breaks Applications – Why Use It? 

_To work around lack of IPv4 address space:_
- Many ISPs have insufficient IPv4 addresses to give their customers a large enough prefix – each customer given one IPv4 address and a NAT 
- Many customers don’t want to pay their ISP for more IPv4 addresses – addresses are scarce, so expensive 
- IPv6 is designed to make addresses cheap and plentiful, to avoid these problems

_To translate between IPv4 and IPv6 addresses:_
- ISP network runs IPv6 only; customers given public IPv6 addresses 
- Translate IPv4\-to\-IPv6 as packets leave private network 
- If destined for IPv4 host on the Internet, translate back to IPv4 on leaving ISP network 
- If destined for IPv6 host on the Internet, forward directly 
- May be useful if ISP has more customers than it has IPv4 addresses

_To avoid re-numbering a network when changing to a new ISP:_
- Hard\-coding IP addresses, rather than DNS names, in configuration files and application is a bad idea 
- Many people do it anyway – makes changing IP addresses difficult 
- IPv6 tries to make renumbering networks easier, by providing better auto\-configuration 
- Some vendors also offer IPv6\-to\-IPv6 NAT

#### Implications of NAT for TCP Connections

_Outgoing connections create state in NAT, so replies can be translated to reach the correct host on the private network_
- Need to send data periodically, else NAT will assume the connection has failed 
- Recommended time out interval is 2 hours, many NATs use shorter

_No state for incoming connections_
- NAT can’t know where to forward incoming connections, without manual configuration 
- Complicates running a server behind the NAT, or peer\-to\-peer applications

#### Implications of NAT for UDP Flows

_Outgoing UDP packets create state in NAT, so replies can be translated to reach the correct host on the private network_
- UDP not connection-oriented; NAT can’t detect the end of a flow, so use short timeout to cleanup state once UDP flow has stopped 
- UDP NAT traversal standards suggest sending a keep-alive every 15 seconds 

_No state for incoming connections_
- UDP NATs often more permissive about allowing incoming packets than TCP NATs; many allow replies from anywhere to an open port – simpler for peer\-to\-peer traffic

#### Peer\-to\-peer NAT Traversal Concepts 

- NATs support outbound connections from client to server 
- Incoming connections fail, since NAT cannot know how to translate the incoming packets 
- Peer\-to\-peer connections can succeed if both NATs think a client server connection is being opened, and the response is coming from the server

_Peers connect to referral server on public network_
- **binding discovery** : Use server to discover the NAT bindings
- **Exchange candidate** : addresses with peer via the referral server 

_Peers systematically probe connectivity, try to establish a connection using every possible combination of addresses_
- Every possible network interface and protocol, mapped and local 
- Complex and generates significant traffic overhead

#### Binding Discovery 

- Packets sent from a host on a private network to a server on the public network will have source IP address and port translated 
- The server can see the translated address/port, and send a reply back to the host telling it the address its packets appear to come from – the server reflexive address 
- Known as NAT binding discovery 
- The STUN Protocol \(session traversal utilities for NAT\) is a standard binding discovery mechanism 

_Host attempts to find every possible candidate IP address, on which it might be reachable_
- The IPv4 and IPv6 addresses of each of its interfaces \(Wi\-Fi, Ethernet, 4G, …\) 
- For each address, any server reflexive addresses discovered using STUN from that address 
- Any relayed addresses \(e.g., via a TURN or SOCKS proxy, VPN server, etc.\)

#### Candidate Exchange

- Each host discovers its candidate IP addresses/ports 

_The peer hosts exchange candidates, using server on the public network that is reachable by both as a relay_
- They make TCP connections to the relay server and exchange data over those connections 
- Why not just send all the data via the relay server? To reduce latency, and to preserve privacy 
- The relay is always aware that communication is being attempted; this communication metadata is potentially sensitive information

#### Probe for connectivity: The ICE Algorithm

_The hosts systematically try connect\(\) from each of their candidate addresses, to every candidate address of their peer_
- Connection requests sent from a host that passes through a NAT will open a binding that allows a response, even if the connection request fails 
- A later incoming connection request that reaches the port on the NAT previous opened by previous outgoing request will pass the NAT, allowing the connection to succeed 
- The hosts then exchange data over the path to confirm success 

_The ICE algorithm, RFC 8445, describes how to do this_

#### Peer\-to\-peer NAT Traversal 

- Binding discovery and systematic connection probing is complex, slow, and generates a lot of unnecessary traffic 

_Effective for UDP traffic_
- Developed to support VoIP applications, that send UDP packets 
- Connectionless nature of UDP means NATs tend to be permissive about allowing incoming packets, provided they reach the correct port 

_Less effective for TCP connections_
- NATs often require an exact match for incoming packets to a previous outgoing TCP packet – addresses, ports, TCP sequence numbers – before they allow a connection to be established

## Week 3
### Slides

#### Numerous Organisations Monitor Internet traffic

* Governments, intelligence agencies, and law enforcement 
 * Good reasons to monitor some traffic
 * Edward Snowden showed pervasive monitoring of all traffic
* Business “Your call may be monitored for quality and training purposes” 
 * Regulatory requirements to record some traffic – e.g., banking 
 * To profile customers for advertising
* Network operators
 * To support network operations and trouble\-shooting
 * To profile customers for advertising
* Criminals and malicious users 
 * Steal data and user credentials; identity theft; active attacks

#### Protecting Privacy

* Mechanisms that protect privacy against malicious attackers will also prevent benign monitoring
* No known way to stop criminals and malicious attackers from accessing private data that doesn’t also stop law enforcement

#### Protecting Message Integrity

* Numerous organisations may want to change messages in transit
 * Governments, intelligence agencies, and law enforcement 
  * Many governments require ISPs to censor or modify DNS responses
  * Many governments require ISPs to censor messages containing certain content
 * Businesses and network operators
  * To enforce legal restrictions on content, terms of service, or to prevent copyright infringement
 * Criminals and malicious users
  * Phishing scams and identity theft
* Mechanisms to protect messages from malicious attackers also prevent benign actors
 * e.g., web browsers deploy DNS-over-HTTPS \(DoH\) to ensure integrity of DNS responses → protects against phishing attacks that modify DNS replies → stops ISPs modifying DNS responses to prevent access to domains hosting illegal material
* No technical way to distinguish beneficial integrity violations from malicious attacks

#### Preventing Protocol Ossification

* Network operators deploy middleboxes to monitor/modify traffic: 
 * NATs, firewalls, monitors, traffic shaping, filtering, etc.
 * Some are necessary and beneficial, others perhaps less so
* Middleboxes must understand protocols used by the network traffic:
 * e.g., NAT has to know where to find IP addresses and ports in packets, if it is to translate them
 * e.g., traffic shapers, that limit TCP throughput for users exceeding their monthly bandwidth use cap, need to parse TCP packets and know how to change them to influence congestion control 
* This can lead to protocol ossification – cannot change end-to-endprotocols, because doing so interacts poorly with middleboxes that don’t understand the changes
* The more of a protocol that is encrypted, the easier it is to change – since middleboxes cannot understand or modify the data – but the harder it is for middleboxes to provide useful services

#### Security and Policy

* Strong reasons to protect privacy, prevent modification in data in transit, and prevent protocol ossification
* The consequences of this protection are sometimes problematic
* Dialogue between engineers, protocol designers, operators, policy makers, and law enforcement crucial – to understand constraints and concerns

#### Goals of Secure Communication

* Goal: deliver message from sender to receiver 
 * Avoid eavesdropping → encrypt to provide confidentiality 
 * Avoid tampering → authenticate to ensure the message is not modified in transit
 * Avoid spoofing → validate identity of sender

#### How to Provide Confidentiality? 

* Data traversing the network can be read by any device on the path
 * Can eavesdrop on packets as they traverse a link
 * Configure a switch or router to snoop on data as it’s forwarded between links
* The network operator can always do this; if their network has been compromised, maybe so can others
* Data can always be read → use encryption to make it useless if intercepted
* Two basic approaches
 * Symmetric cryptography
  * Advanced Encryption Standard \(AES\)
 * Public key cryptography
  * The Diffie\-Hellman algorithm 
  * The Rivest-Shamir\-Adleman \(RSA\) algorithm
  * Elliptic curve\-based algorithms 

#### Symmetric Cryptography

**Symmetric encryption converts plain text into cipher\-text**  
* A secret key control the encryption and decryption process 
 * Same key used to encrypt as is used to decrypt
 * Provided the key is secret and only known to sender and receiver, the conversation is secure – problem: how to securely distribute the key?
* Very fast – suitable for bulk encryption
* Encryption and decryption algorithms are public

#### Public Key Cryptography

**Public key encryption also converts plain text into cipher\-text**  
* Again, the algorithms are public:
 * Diffie–Hellman 
 * Rivest–Shamir–Adleman \(RSA\)
 * Ephemeral Elliptic Curve Diffie\-Hellman
* Public key algorithms use two related keys: 
 * The public key for a user is widely distributed
 * The corresponding private key must be kept secret
 * If one key is used to encrypt, the other key is needed to decrypt the message 
* Solves key distribution problem 
 * Look\-up the public key of the receiver in a directory 
 * Sender uses the public key to encrypt the message → can only be decrypted by the private key 
 * If receiver is trusted to keep private key secret, only it can decrypt the message
* Problem: very slow to encrypt and decrypt

#### Hybrid Cryptography

* Modern communications use a combination of both public\-key and symmetric cryptography for security and speed 
 * Sender chooses a random value, K<sub>s</sub>, that can be used as key for the symmetric encryption algorithm 
 * Sender looks up the receiver’s public key, K<sub>pub</sub>, uses it to encrypt K<sub>s</sub>, and sends the result to the receiver; receiver uses the corresponding private key, K<sub>priv</sub>, to decrypt the message and retrieve K<sub>s</sub>
  * Securely transfers K<sub>s</sub> from sender to receiver 
  * Public key encryption is very slow, but the key K<sub>s</sub> is small, so this doesn’t matter
 * Sender encrypts future messages using symmetric cryptography with key K<sub>s</sub>, receiver also has k<sub>s</sub>, which it uses to decrypt the messages
  * Symmetric cryptography is fast, but requires the key to be exchanged securely
  * The public key algorithm has been used to securely exchange the key 
* Ensures confidentiality of communication with good performance

#### Authentication

**Encryption can ensure confidentiality – but also need to verify identify of sender and ensure messages have not been modified in transit**  
* Generate a digital signature to authenticate the message 
* Relies on public key cryptographic and a cryptographic hash

#### Cryptographic Hash Function

* Cryptographic hash takes arbitrary input and produces a fixed length output hash
 * Any change to input generates different output 
 * Infeasible to find two inputs that give the same output 
 * Calculating a cryptographic hash is fast
 * Reversing a hash, to find the input given only the output, is infeasible
* Many cryptographic hash algorithms exist: 
 * Recommendation: SHA256 algorithm
 * Older algorithms, e.g., MD5 and SHA1, have known security flaws

#### Digital Signatures

* Sender generates a digital signature
 * Sender calculates the cryptographic hash of the message 
 * Sender encrypts the hash with their own private key
  * Anyone can use the sender’s public key to decrypt this, but only the sender can have encrypted it \(if trusted to keep their private key secret\) 
 * Attaches encrypted hash to the message
* Message and its digital signature are encrypted and sent to receiver using hybrid encryption
* Signature verification process:
 * Receiver decrypts the message 
 * Receiver calculate cryptographic hash of the message 
 * Receiver decrypts digital signature using sender’s public key, to find the hash that the sender calculates 
 * If hash decrypted hash and the hash calculated by the receiver match, then the message is authentic and unmodified – provided the sender kept its private key secret

#### Trust and Public Key Infrastructure

* How to know what public key corresponds to a particular receiver?
 * The receiver gave you their key in person 
 * The receiver sent you their key, authenticated by someone you trust
 * Someone you trust gave you the receiver’s key
* A public key infrastructure can authenticate keys
 * PKI verifies sender’s identity, then adds their digital signature to sender’s public key
 * If receiver trusts PKI, can verify the digital signature to confirm identity of sender

#### Transport Layer Security \(TLS\) v1.3

* TCP is not secure – neither the TCP/IP headers nor the data are encrypted or authenticated 
* The Transport Layer Security protocol \(TLS v1.3\) can be used to encrypt and authenticate data carried within a TCP connection 

#### TLS v1.3 Overview

* A TCP connection is established 
* TLS handshake protocol runs within that TCP connection
 * Authenticates endpoints and agrees on the encryption keys to use
* TLS record protocol then runs over the TCP connection, lets endpoints exchange authenticated and encrypted blocks of data
 * TLS turns the TCP byte stream into a series of records → provides framing

#### TLS v1.3 Handshake Protocol

* TCP connection established as usual
 * SYN→SYN\+ACK→ACK
* TLS handshake protocol immediately follows 
 * TLS ClientHello sent with the ACK
 * TLS ServerHello sent in response 
 * TLS Finished message concludes, and carries initial secure data record 
* Adds 1\-RTT to connection establishment

#### TLS v1.3 ClientHello

**The ClientHello message:**  
* Indicates that TLS v1.3 is to be used
 * Signals TLS v1.2 in the main ClientHello message, with an extension header to say “I’m really TLS v1.3” because too many middleboxes break if the TLS version changes – protocol ossification
* Provides the cryptographic algorithms the client supports 
* Provides the name of the server to which the client is connecting
 * If connecting to a web hosting server, it’s likely that more than one site is hosted on the same server, so need to specify which is intended
* Does not contain any data

#### TLS v1.3 ServerHello

**The ServerHello message:**  
* Indicates that TLS v1.3 is to be used 
 * It signals TLS v1.2 in the main ServerHello message, and includes an extension header to say “I’m really TLS v1.3” because too many middleboxes break if the TLS version changes – protocol ossification
* Provides cryptographic algorithms selected by the server, from the set the client suggested 
* Provides the server’s public key and digital signature used to verify its identity 
* Does not contain any data

#### TLS v1.3 Finished

**The Finished message:**  
* Provides the client’s public key
* Optionally, provides the certificate needed to authenticate the client to the server 
* May contain data sent from client to server

#### TLS v1.3 Cryptographic Algorithms

* Client and server use the Ephemeral Elliptic Curve Diffie\-Hellman \(ECDHE\) key exchange algorithm 
 * Client sends its public key to server in ClientHello
 * Server sends its public key to client in ServerHello
 * Client and server both combine the two public keys to derive the key used for the symmetric cryptography – complex mathematics; will not describe
 * Server provides a certificate \(digital signature\) to allow the client to verify its identify in the ServerHello – client can optionally provide this in Finished
* Client proposes symmetric encryption algorithms in ClientHello, server picks from them and replies in ServerHello
 * Either AES or ChaCha20 symmetric encryption

#### TLS v1.3 Record Protocol

* TLS v1.3 splits the data into records, each containing ≤ 2<sup>14</sup> bytes
 * Each record is both encrypted and authenticated; it has a sequence number
 * Can renegotiate encryption keys between records 
 * TCP does not preserve record boundaries; TLS adds framing so that it does – reading from a TLS connection will block until a complete record is received
* Client and server exchange records – send and receive data – then close connection

#### TLS v1.3 0\-RTT Mode

* TLS v1.3 usually takes 1\-RTT to establish a connection, after TCP connection setup 
* If a client and server have previously communicated, they can re\-use a key: 
 * Server can send additional encryption keys as part of ServerHello, that client can use the next time is connect to that server
 * On next connection, ClientHello message can include data to be delivered to the server, encrypted with that pre-shared key; the ServerHello can contain a reply 
 * This 0\-RTT data may be delivered more than once, if the ClientHello or ServerHellomessages are duplicated – TLS doesn’t stop this
  * Protection against duplicate messages is provided by sequence numbers in the record layer 
  * Handshake messages do not have sequence numbers, so duplicated messages can deliver data more than once 
  * **Be careful writing applications that use 0\-RTT mode**

#### Limitations of TLS

**TLS issecure, but has limitations:**  
* Does not encrypt server name:
 * Exposes hostname of server to which connection is being made 
 * Encrypted SNI extension in development – difficult to deploy
* Operates within a TCP/IP connection:
 * IP addresses and TCP port numbers are not protected – exposes information about who is communicating and what application is being used
* Relies on a PKI to validate public keys:
 * Significant concerns about trustworthiness of PKI
* May deliver 0\-RTT data more than once

#### End\-to\-end Security?

* For communication to be secure, it must be end\-to\-end
* The two endpoints are the sender and the final recipient
    * With a data centre or CDN, what is the final recipient?
     * Is it the load balancer at the entrance to the data centre, or the server within the data centre that processes the request? 
     * If the request is directed to a content distribution network \(CDN\), is the end the local cache that serves the request? If so, how are the encryption keys shared? 
 * If the data is moving between two users, is it encrypted between the two users or between each user and the data centre?
     * i.e., can the data centre see user-to-user data flows?
     * This is normal if you run TLS from user\-to\-data centre then from data centre\-to\-user
* Is there in\-network processing? How much data is revealed to the in\-network server?
    * e.g., video conference with privacy protection vs. without 
    * Does the central server decrypt the speech data, mix into one stream and send to the receiver, or does it forward all active streams in encrypted form
    * Trades\-off security vs bandwidth 
    * For audio the bandwidth is small enough this doesn’t matter
    * For video conferencing, the combined bandwidth may be significant

#### The Robustness Principle (Postel’s Law)

At every layer of the protocols, there is a general rule whose application can lead to enormous benefits in robustness and interoperability:

“Be liberal in what you accept, and conservative in what you send"

Software should be written to deal with every conceivableerror, no matter how unlikely; sooner or later a packet willcome in with that particular combination of errors andattributes, and unless the software is prepared, chaos canensue.  In general, it is best to assume that the network is filled with malevolent entities that will send in packets designed to have the worst possible effect.  This assumptionwill lead to suitable protective design, although the most serious problems in the Internet have been caused by un\-envisaged mechanisms triggered by low\-probability events;mere human malice would never have taken so devious a course!

_Balance interoperability with security – don’t be too liberal in what you accept; a clear specification of how and when you will fail might be more appropriate_

#### Validating Input Data

* Networked applications work with data supplied by un\-trusted third parties 
* Data read from the network may not conform to the protocol specification 
* Due to ignorance, bugs, malice, or a desire to disrupt services 
* **Must carefully validate all data before use**

#### Writing Secure Code

* The network is hostile: any networked application is security critical 
    * Must carefully specify behaviour with both correct and incorrect inputs
    * Must carefully validate inputs and handle errors
    * Must take additional care if using type\- and memory\-unsafe languages, such as C and C\+\+, since these have additional failure modes
* **The best encryption doesn’t help if the endpoints can be compromised**

## Week 4
### Slides
#### Limitations of TLS v1.3

**TLS v1.3 is a tremendous success**  
* Significant security improvements compared to TLS v1.2
	* Removed support for older and less secure encryption and key exchange algorithms
	* Removed support for secure algorithms that have proven difficult to implement correctly
* Some performance improvements to the initial handshake and with 0\-RTT mode  
**Despite this, TLS v1.3 has some limitations that are hard to fix**  
* Connection establishment is still relatively slow 
* Connection establishment leaks potentially sensitive metadata
* The protocol is ossified due to middlebox interference

#### TLS v1.3 Connection Establishment Performance

* TCP connection established as usual: 
	* SYN → SYN\+ACK → ACK
* TLS handshake protocol runs inside TCP connection:
	* TLS ClientHello sent with final ACK
	* TLS ServerHello sent in response
	* TLS Finished message concludes, and carries initial secure data record 
* First data sent 2x RTT after connection establishment starts 
* Earliest response received 3x RTT after connection establishment starts

* Average web page comprises 1.7 MB of data, fetched as 69 HTTP requests, using 15 TCP connections
* 83% of HTTP requests run over TLS 
* **Enormous amount of time wasted, waiting for TCP and TLS connection establishment handshakes**
* Can we speed up TLS connection setup?
	* 0\-RTT Connection Reestablishment – speed\-up connections to known servers 
	* Concurrent TCP and TLS handshake – speed\-up connections to all servers

#### 0\-RTT Connection Reestablishment 

* Common to connect to a previously known TLS server – is it possible to shortcut the connection establishment in such cases?

**What is the role of the TLS handshake?**  
* Uses public key cryptographic techniques to establish an ephemeral session key, used to encrypt the data 
	* The ClientHello and ServerHello are used to exchange material used to derive a session key – using ECDHE key negotiation 
	* The session is ephemeral – different for each connection; derived from the public keys and a random value
	* The ephemeral session key provides forward secrecy – each connection has a unique key; if the encryption key for one session leaks, it doesn’t help an attacker break other sessions 
* Retrieve the server’s certificate, allowing the client to authenticate the server 
	* The ServerHello contains the certificate

**How to encrypt initial data?**  
* Cannot negotiate ephemeral session key for initial data → relies on data exchanged in the handshake 
	* Reuse a pre\-shared key agreed in previous TLS session 
* In a previous TLS connection
	* Server sends a PreSharedKey with a SessionTicket to identify the key
* When reestablishing a connection: 
	* Client sends SessionTicket, data encrypted using corresponding PreSharedKey, along with ClientHello
	* The server uses SessionTicket to find saved PreSharedKey, decrypt the data 
	* ClientHello and ServerHello complete usual key exchange; data sent with ServerHello and later protected using ephemeral session key → no additional round\-trips due to TLS

**What are the potential risks?**  
* 0\-RTT data sent with ClientHello using a PreSharedKey is not forward secret 
	* Use of PreSharedKey links TLS connections – if session where PreSharedKey is distributed is compromised, 0\-RTT data sent using that key in future connections will also be compromised
* 0\-RTT data sent with ClientHello using a PreSharedKey is subject to replay attack
	* The 0\-RTT data is accepted during TLS connection establishment 
	* If on\-path attacker captures and replays the TCP segment with the ClientHello, SessionTicket, and data protected with the PreSharedKey, that data will be accepted by the server again
	* The server will respond to the replay, trying to complete the handshake – this might fail
	* But – by then, the data will have been accepted 
	* Ensure 0-RTT data is idempotent to avoid this risk   
**Be very careful using 0-RTT data in TLS v1.3 – trades performance for safety**

#### TLS v1.3 Metadata Leakage

* IP exposes addresses
* TCP exposes port numbers and connection metadata
* When TLS is used with HTTPS, ClientHello includes the Server Name Indication \(SNI\) extension
	* Identifies requested site, so server knows what public key to use in ServerHello
	* Required to support shared hosting, with multiple websites on one server 
	* Has to be unencrypted – sent before session keys are negotiated 
	* Can’t encrypt with PreSharedKey, since that’s provided by server, and goal is to select the server 

#### TLS v1.3 Protocol Ossification

* TLS is widely implemented, but many poor quality implementations: 
	* Some TLS servers fail if ClientHello uses unexpected version number, rather than try to negotiate older version 
	* Some firewalls block connections if ClientHello is structured differently to that used by TLS 1.2 and earlier, even if TLS 1.3 is signalled 
* Original design of TLS 1.3 changed ClientHello
	* Updated the version number \(1.2 → 1.3\)
	* Removed some now unused header fields 
	* Measurements showed this caused \~8% of TLS 1.3 connections to fail

* Later versions of TLS 1.3 changed the design to work around these bugs
	* Version number in ClientHello says TLS 1.2; unused header fields present with dummy values; extension header to ClientHello signals actual version
	* \(Similar changes in ServerHello\) 
	* When TLS 1.3 client talks to TLS 1.3 server, version negotiated in extensions 
	* When TLS 1.3 client talks to TLS 1.2 server, extension ignored and TLS 1.2 is negotiated
* Protocol ossification is a significant concern
	* TLS is not the only protocol to include such workarounds
	* Widely deployed faulty implementations constrain design of most protocols

#### How to Avoid Protocol Ossification?

* Ossification happens when extension mechanisms, or allowed flexibility, are not used 
	* TLS 1.3 was released ten years after TLS 1.2 
	* Allowed products to be built and deployed that didn’t do version negotiation correctly, since no new versions to negotiate
	* Allowed products to be built that relied on the presence and order of fields in ClientHello, since all implementations included the same fields in the same order
* Generate Random Extensions And Sustain Extensibility \(GREASE\) 
	* If the protocol allows extensions, send extensions
	* If the protocol allows different versions, negotiate different versions 
	* Do this even if you don’t need to → “use it or lose it”
	* Send meaningless dummy extensions that are ignored 
	* Change the version number to prove you can

#### QUIC: Performance, Security, Avoiding Ossification

* What’s wrong with TLS v1.3 over TCP? 
	* Slow to connect – due to sequential TCP and TLS handshakes
	* Leaks some metadata 
	* Ossified and hard to extend
* QUIC aims to replace TLS v1.3 and TCP with a single secure transport protocol 
	* Reduce latency by overlapping TLS and transport handshake 
	* Avoid metadata leakage via pervasive encryption
	* Avoid ossification via systematic application of GREASE and encryption

#### QUIC Overview 

* QUIC replaces TCP, TLS, and parts of HTTP 
	* HTTP → stream multiplexing 
	* TLS → security
	* TCP → reliability, ordering, congestion control
	* Runs on UDP for ease of deployment
* QUIC is a general purpose client\-server transport 
	* Designed to run HTTP effectively

#### QUIC Packets, Headers, and Frames

* QUIC sends and receives streams of data within a connection 
	* Up to 2<sup>62</sup> different streams in each direction in a single QUIC connection
* A connection comprises QUIC packets sent within UDP datagrams 
* Each QUIC packet starts with a header, and contains one or more frames 
	* Frames contain data for streams, or acknowledgements, or other control messages

#### QUIC Headers

* QUIC packets can be long header packets or short header packets
* Long header packets are used to establish QUIC connections
	* They all start with a common header, followed by packet\-type specific data
* Four different long-header packet types, denoted by the TT field in the header: 
	* Initial – initiates connection, starts TLS handshake 
	* 0\-RTT – idempotent data sent with initial handshake, when resuming a session 
	* Handshake – completes connection establishment 
	* Retry – used to force address validation
* Several Initial, 0\-RTT, and handshake packets can be included in one UDP datagram, one after the other, followed by a short header packet

* The is one short header packet defined in QUIC:
	* 1\-RTT – Used for all packets sent after the TLS handshake is complete 
	* The short header is followed by QUIC frames in the enclosing UDP packet 
	* Compared to long header, omits information that can be inferred from context

#### QUIC Frames

* QUIC packet contain an encrypted sequence of frames
	* CRYPTO frames are used to carry TLS messages such as the ClientHello, ServerHello etc.
	* STREAM and ACK frames send data and acknowledgements 
	* Migration between two network interfaces is supported by PATH_CHALLENGE and PATH_RESPONSE frames
	* Other frames control progress of a QUIC connection 
* Compared to TCP, QUIC headers are limited in scope 
	* Functionality provided by frames instead → more extensible
	* e.g., TCP sends sequence numbers and acknowledgements in the header; QUIC sends this information in STREAM and ACK frames

#### QUIC Connection Establishment and Data Transfer

* A QUIC connection proceeds in two phases: handshake and data transfer 
	* The handshake uses long header packets – establishes the connection, negotiates encryption keys, authenticates the server
	* The data transfer phase uses short header packets – sends data and acknowledgements after the connection is established

#### QUIC Connection Establishment 

**QUIC combines connection establishment and TLS handshake into one round\-trip**  
* C → S: QUIC Initial packet 
	* Initial packet contains a CRYPTO frame that contains TLS ClientHello
* S → C: QUIC Initial and Handshake packets 
	* Both QUIC packets can be sent in a single UDP datagram 
	* Initial packet contains CRYPTO frame that contains TLS ServerHello
	* Handshake packet contains other connection setup information 
* C → S: QUIC Initial, Handshake, and 1\-RTT packets 
	* All three QUIC packets can be sent in a single UDP datagram 
	* QUIC Initial packet contains ACK frame, acknowledging the server’s Initial packet
	* QUIC Handshake packet contains CRYPTO frame that contains TLS Finished
	* QUIC 1\-RTT \(short header\) packet contains STREAM frame with initial data sent from client to server

* QUIC Initial packets play two main roles: 
	* Synchronise client and server state – like TCP’s SYN and SYN\+ACK packets
	* Contains CRYPTO frame, with TLS ClientHello or Finished, and may also contain ACK frame 
	* Combines connection setup and security negotiation in one packet 
* QUIC Initial packets also carry optional Token
	* Server can refuse the initial connection attempt, and send a Retry packet containing a Token
	* Client must then retry the connection, providing the Token in its Initial packet 
	* Can be used to prevent connection spoofing

* QUIC Handshake packets complete the TLS 1.3 exchange 
	* The TLS ServerHello and Finished messages
	* TLS can also renegotiate new keys part\-way through a connection – this is done in Handshake packets

* QUIC supports TLS 0-RTT session re\-establishment:
	* QUIC Initial packet contains CRYPTO frame with a TLS ClientHelloand a SessionTicket
	* QUIC 0\-RTT packet included in the same UDP datagram contains a STREAM frame carrying idempotent 0\-RTT data: 
	* Server responds with data in 1\-RTT \(short header\) packet, along with its Initial and handshake packets

_QUIC combines connection establishment and encryption key negotiation into a single handshake → TLS\-over\-TCP runs them sequentially._

#### Data Transfer, Streams, and Reliability

**After handshake has finished, QUIC switches to sending short header packets**  
* The short header contains a Packet Number field
	* Packet numbers increase by one for each packet sent; ACK frames indicate received packet numbers
	* QUIC packet numbers count packets sent; TCP sequence numbers count bytes of data sent
	* QUIC never retransmits packets – retransmits frames sent in lost packets in new packets, with new packet numbers 
	* TCP retransmits lost packet with original sequence number
* Protected payload section of short header packets contains encrypted QUIC frames
	* STREAM frames contain data 
	* ACK frames contain acknowledgements
* Performs congestion control as in TCP

* QUIC sends acknowledgements of received packets in ACK frames
	* Sent inside a long\- or short\-header packets; unlike TCP, not part of headers 
	* Indicate sequence numbers of QUIC packets that were received, not frames

**Data is sent within STREAM frames, sent within QUIC packets**  
* Contain a stream identifier, offset of the data within the stream, data length, and data 
* QUIC provides multiple reliable byte streams within a single connection 
	* Data for each stream is delivered reliably and in\-order 
	* Order is not preserved between streams
	* Avoids head\-of\-line blocking between streams
* Can view QUIC streams as multiple unframed byte streams sent within a single connection; alternatively can view each stream as framing a message, and the connection as a series of messages

#### QUIC over UDP

**Why run QUIC over UDP rather than over IP?**  
* To ease end\-system deployment in user\-space applications
* User\-space applications, running over UDP, are easy to build 
	* BSD sockets; portable → same API works everywhere 
	* Widely understood programming model 
	* No need for privileged access
* No portable, unprivileged, interface to build applications that run directly over IP
	* Implementations have to run within the operating system kernel
	* Deploying kernel updates is difficult 
	* Deploying application updates is straightforward 
* To work around protocol ossification due to middleboxes
	* Firewalls block anything other than TCP and UDP

#### Ossification 

* Deployment experience → if a field in a protocol is visible to the network, someone will implement a middlebox that relies on its presence 
* Once a protocol has been widely deployed, very hard to change

* Protocol ossification affected the design of: 
	* TLS 1.3 
	* Multipath TCP
	* TCP Fast Open 
	* TCP Selective Acknowledgements
* Increasingly viewed as a problem in the standards community 
	* Difficult to evolve network protocols to address new requirements 
	* A system that can no longer evolve and change will die

#### Avoiding Ossification in QUIC

* Three tools to prevent ossification of QUIC: 
	* Published protocol invariants 
	* Pervasive encryption of transport headers
	* GREASE
* QUIC is a new design – want to avoid ossification, starting with initial deployments
* Design the protocol to make it difficult, ideally impossible, for middleboxes to interfere with QUIC connections

#### QUIC Invariants

* Properties of QUIC that will remain unchanged as new versions of the protocol of developed
	* Explicit guidance to middlebox designers: can assume these properties of QUIC will not change
	* The IETF will change other fields or properties between QUIC versions

_What invariants are guaranteed?_  
* Packets start with a long header or a short header 
	* The first bit of long header packets is always 1; they include version number, destination\- and source\-connection identifiers
	* The first bit of short header packets is always 0; they include a destination connection identifier 
* Connections can arbitrarily switch between long header and short header packets

#### Avoiding Ossification via Pervasive Encryption

**QUIC encrypts as much data as possible**  
* Entire packet except invariant fields and the last 7\-bits of the first byte is encrypted; entire packet is authenticated 
* Encryption keys for initial handshake packets are derived from connection identifiers
	* Contain ClientHello and ServerHello, which are unencrypted when using TLS over TCP, and don’t need to be encrypted
	* QUIC provides no more security than TLS over TCP, but makes it expensive for middleboxes to read handshake
* Rest of QUIC connection protected by TLS 1.3 as normal 
* QUIC authenticates all data
	* If a middlebox changes the headers, the change can be detected

#### Avoiding Ossification via GREASE

**QUIC makes extensive use of GREASE**  
* Every field encrypted or has a value that is unpredictable
	* New connections use randomly chosen connection identifies
	* Clients randomly try to negotiate new version numbers 
	* Version numbers matching 0x?a?a?a?a for testing version negotiation – will be rejected by servers 
	* Unused header fields given randomly chosen values
* Goal is that middleboxes can’t make any assumptions about QUIC header values → nothing in the header is predictable 
* Hopefully avoids ossification → nothing to ossify around

#### QUIC Benefits and Costs

* Why is QUIC desirable?
	* Reduces secure connection establishment latency
	* Reduces risk of ossification; easy to deploy
	* Supports multiple streams within a single connection 
* Why is QUIC problematic?
	* Libraries and support new, poorly documented, and frequently buggy
	* CPU usage is high compared to TLS\-over\-TCP 
	* These issues will be resolved – but it will take some years before QUIC is as stable and performant as TLS\-over\-TCP 

_TCP lasted 40 years – QUIC is a similarly long-term project, that’s only just reaching version 1.0._

## Week 5
### Slides
#### Packet Loss in the Internet

**The Internet is a best effort packet delivery network – it is unreliable**  
* IP packets may be lost, delayed, reordered, or corrupted in transit 
* How often this happens varies significantly
	* Wireless links are less reliable than wired links
	* Countries with well\-developed infrastructure tend to have reliable Internet links; countries with less robust or lower capacity infrastructure tend to see more problems
	* Some protocols intentionally try to push links to capacity, causing temporary overload as they try to find the limit 
	* Some packet loss is inevitable  
_The transport layer must adapt the quality of service provided by the network to match application needs._

#### The End\-to\-End Argument

**Is it better to place functionality within the network or at the end points?**  
* Only put functionality that is absolutely necessary in the network, leave everything else to end systems
	* Example: let the network provide best effort packet delivery, rather than try to detect and retransmit lost packets 
	* If the network is not guaranteed to be 100% reliable, always, end systems must check for lost packets anyway
	* Since 100% reliability can never be guaranteed, no point in complicating thenetwork trying to make it reliable 
* One of the defining principles of the Internet

#### Timeliness vs Reliability Trade\-off 

* Repairing or retransmitting lost packets takes time
* Fundamental trade\-off: 
	* If a connection is to be reliable, it cannot guarantee timeliness
	* If a connection is to be timely, it cannot guarantee reliability
* Different applications make different timeliness vs. reliability trade\-offs:
	* Web, email, etc. → data must be delivered in order sent; no strong timeliness requirement
	* Telephony and video conferencing → tolerates some data loss, but requires timeliness 
* Implication for network architecture: 
	* Network layer should provide a timely but unreliable service
	* Transport layer protocols can add reliability, if needed

#### Packet Loss and UDP

* UDP → unreliable, connectionless, datagram service
	* Adds port numbers and a checksum to IP
	* Does not provide reliability or congestion control – best effort packet delivery 
* A substrate for building new transport protocols
	* QUIC
	* RTP
	* DNS 

#### Sending UDP Datagrams

* The sendto\(\) call sends a single datagram 
* Each call to sendto\(\) can send to a different address, even though they use the same socket
* Alternatively, connect\(\) to an address, then use send\(\) to send the data 
	* There is no connection made by the UDP layer, a connect\(\) call only sets the destination address for future packets

#### Receiving UDP Datagrams

* The recv\(\) call may be used to read a single datagram, but doesn’t provide the source address of the datagram
* Most code uses recvfrom\(\) instead – this fills in the source address of the received datagram
* Packets can be lost, delayed, or reordered in transit – UDP does not attempt to recover from this

#### UDP Framing and Reliability

* Each sendto\(\) calls generates exactly one UDP datagram
	* Each recvfrom\(\) corresponds to a single sendto\(\)
* But, UDP is unreliable: 
	* Datagrams may be lost, delayed, reordered, or duplicated in transit 
	* Data sent with sendto\(\) might never arrive 
	* Data sent with sendto\(\) might arrive more than once
	* Data sent in consecutive calls to sendto\(\) might arrive out\-of\-order
	* UDP does not attempt to correct this
* The protocol built on UDP is responsible for correcting the order, detecting duplicates, and repairing loss – if necessary 
	* The protocol running within UDP generally includes a sequence number to support this
	* e.g., RTP and QUIC both include a packet sequence number inside UDP packets
* UDP provides framing – data is delivered a packet at a time – but is unreliable
* Application must organise the data so it’s useful if some datagrams lost 
	* e.g. video conferencing with I\- and P\-frames

#### UDP Sequencing and Reliability

**UDP does not attempt to provide sequencing, reliability, or timing recovery**  
* It provides a best\-effort datagram delivery service, and identifies applications according to port numbers – substrate on which application protocols can be implemented 
* The syntax and semantics of the datagrams depends on the application layer protocol running within UDP
	* This might provide sequence numbers and acknowledgements 
	* This might provide retransmission and/or forward error correction
	* This might provide timestamps to recover timing
	* This might provide payload identification, or other information

#### TCP Service Model

**Refer to 05c**

#### Reliable Data Transfer with TCP

* TCP delivers an ordered, reliable, byte stream
* After connection established, client and server can send\(\) or recv\(\) data 
	* Data can flow in either direction within a TCP connection
	* No requirement that data transfers follow a request\-response pattern; client and server can send in any order
* TCP ensures data delivered reliably and in order 
	* TCP sends acknowledgements for segments as they are received; retransmits lost data
	* TCP will recover original transmission order if segments are delayed and arrive out of order

#### Reading and Writing Data on a TCP Connection 

* The send\(\) function transmits data
	* Blocks until the data can be written
	* Might not be able to send all the data, if the connection is congested 
	* Returns actual amount of data sent
	* Returns \-1 if error occurs, sets errno
* The recv\(\) function receives data 
	* Blocks until data available or connection closed; reads up to BUFLEN bytes 
	* Returns number of bytes read 
	* If connection closed, returns 0 
	* If error occurs, returns \-1 and sets errno
	* Received data is not null terminated \- **This is a significant security risk**

#### TCP Segments and Sequence Numbers

* The send\(\) call enqueues data for transmission
* Data is split into segments, each placed in a TCP packet
* TCP packets sent in IP packets, when allowed by congestion control algorithm  
	* Each segment has a sequence number
	* Sequence numbers start from the value sent in the TCP handshake 
	* Initial sequence number is sent in first packet sent from client→server \(the packet that has the SYN bit set to 1\); chosen randomly by the client 
	* First data packet has sequence number one higher than the initial packet 
	* Subsequent data packets increase sequence number by number of bytes sent
* Separate sequence number spaces in each direction

* Calls to send\(\) don’t directly map to TCP segments 
	* If data given to send\(\) is too large to fit in one segment, TCP will split it across several segments 
	* If data given to send\(\) is small, TCP might wait to send the data, combining it with later data into a single larger segment
	* Known as Nagle's algorithm – improves efficiency, but adds some delay 
* Implication: data returned by recv\(\) does not always correspond to a single send\(\) call

#### TCP Does Not Preserve Message Boundaries

* The recv\(\) call returns data reliably, and in the order sent, but doesn’t frame data 
	* Desirable if one recv\(\) call would fetch all the HTTP headers, then another the entire body 
	* TCP not does guarantee this – might split the response arbitrarily, e.g., matching the colours 
	* Complicates code using TCP 
* Implication: you must parse the data to know how much remains to be read

#### TCP Acknowledgements

**TCP receiver acknowledges each segment received**  
* Each TCP segment has sequence number and acknowledgement number
* Segments sent to acknowledge each received segment – contains acknowledgment number indicating sequence number of the next contiguous byte expected 
	* Includes data if any ready to send, or can be empty apart from acknowledgement 
* If a packet is lost, subsequent packets will generate duplicate acknowledgements 
	* In example, segment with sequence number 8 is lost 
	* When segment with sequence number 9 arrives, the receiver acknowledges 8 again – since that’s still the next contiguous sequence number expected
* Can send delayed acknowledgements
	* e.g., acknowledge every second packet if there is no data to send in reverse direction

#### TCP Acknowledgements: Loss Detection 

* TCP uses acknowledgements to detect lost segments 
	* If data is being sent, but no acknowledgements return, then either receiver or the network failed
	* TCP treats a timeout as an indication of packet loss and retransmits unacknowledged segments
* TCP uses acknowledgements to detect lost segments
	* Duplicate acknowledgements received → some data lost, but later segments arrived 
	* TCP treats a triple duplicate acknowledgement – four consecutive acknowledgements for the same sequence number – as an indication of packet loss 
	* Lost segments are retransmitted

**Why a triple duplicate acknowledgement?**  
* Packet delay leading to reordering will also cause duplicate acknowledgement to be generated
* Gives appearance of loss, when the segments are merely delayed 
* Use of triple duplicate ACK to indicate packet loss stops reordered packets from being unnecessarily retransmitted
	* Packets delayed enough to cause one or two duplicate acknowledgements is relatively common 
	* Packets being delayed enough to cause three or more duplicates is rare 
	* Balance speed of loss detection vs. likelihood of retransmitting a packet that was merely delayed

#### Head\-of\-line Blocking in TCP

* A TCP receiver will wait for missing data to be retransmitted
* Calls to recv\(\) block until missing data arrives; TCP always delivers data to the application in a contiguous, ordered, sequence
* Head\-of\-line blocking increases total download time 
* Delay depends on relative values of RTT and packet serialisation delay
* Head\-of\-line blocking increases latency for progressive and real\-time applications
* Significant latency increase if file is being played out as it downloads

#### Reliable Data Transfer with TCP

**TCP provides an ordered, reliable, byte stream service**  
* Service model is simple to understand – it’s like reading from a file 
* Head of line blocking can significantly impact progressive and real\-time uses 
	* MPEG DASH \(“Dynamic Adaptive Streaming over HTTP”\)
* Lack of framing can complicate application design

#### QUIC Service Model

* TCP delivers reliable, ordered, byte stream 
* QUIC delivers several ordered reliable byte streams within a single connection
	* Each stream is delivered reliably and in\-order 
	* Order is not preserved between streams within a QUIC connection

#### QUIC Packets and Sequence Numbers

**Each QUIC packet has a Packet Number**  
* Two packet number spaces
	* Packets sent during initial handshake 
	* Packets sent to carry data 
* Within each space, packet number starts at zero, increases by one for each packet sent
	* Counts number of packets sent
	* Different to TCP, where the sequence number records the offset within the byte stream  
**Each QUIC packet contains one or more frames**  
* STREAM frames carry data
* Each has a stream identifier, and carries the length of the data and its offset from start of stream – closer to TCP sequence numbers

**QUIC doesn’t preserve message boundaries in streams**  
* If data written to stream is too big for a packet, it will be split across multiple packets
* If data written to stream is too small for a packet, it may be delayed and sent with other data to fill complete packet
* Data from more than one stream might be sent in a single packet 
* If \>1 stream has data to send, the QUIC sender can choose how to prioritise and deliver frames from each stream

#### QUIC Acknowledgements

* A QUIC receiver sends acknowledgements for packets it receives 
	* Unlike TCP, it does not acknowledge sequence numbers within each stream 
	* The sender needs to remember what data from each stream was in each packet, to know what parts of each stream have been received
* Acknowledgements sent as reverse path frames
* Acknowledgements can be delayed
	* e.g., send acknowledgement after every second packet is received 
	* The ACK Delay field measures this delay to allow accurate network RTT calculation 
* Acknowledgements contain ranges 
	* e.g., a single ACK Frame can indicate that packets 1\-4 and 6\-8 were received
	* Like TCP Selective Acknowledgement extension

#### QUIC Retransmissions and Loss Recovery

* QUIC does not retransmit lost packets 
	* Every packet has a unique packet number and is only transmitted once
	* Packets declared lost when at least three later packets have been acknowledged \- _Equivalent to TCP triple duplicate ACK_
	* Packets declared lost after timeout – like TCP
* QUIC retransmits lost data in new packets
	* Packetisation of STREAM frames into packets may differ when data retransmitted 
	* Data ordering between streams not preserved

#### Head\-of\-Line Blocking in QUIC

**QUIC can deliver several streams within a single connection**  
* Data for each stream is delivered reliability and in\-order 
	* Whether packet loss affects one or more streams depends how the sender chooses to distribute stream data between packets 
		* Each QUIC packet can contain data from one stream, alternating between streams 
		* Each QUIC packet can contain data from each stream 
		* The specification places no requirements on how streams are split across packets
	* Depending on loss patterns, each stream can independently suffer head-of-line blocking 
		* Affects performance of that stream in the same way head-of-line blocking affects TCP
* Order is not preserved between streams within a QUIC connection
	* One stream might be blocked waiting for a retransmission, while other streams continue to deliver data without loss
	* Data from different streams is sent and received independently → careful use of streams can limit duration of head\-of\-line blocking

#### Reliable Data Transfer with QUIC

* QUIC delivers several ordered reliable byte streams within a single connection 
	* Can be treated like several parallel TCP connections → instead of opening several TCP connections to a server, open one QUIC connection and send multiple streams within it
	* Can be treated as a framing device → each stream represents a single object, with end-of-stream signalling the object is complete
	* Order is not preserved between streams within a QUIC connection
* Best practices for use of multiple streams are still evolving

## Week 6

#### TCP Congestion Control

* Congestion control principles
* Loss\-based congestion control 
	* How to effectively make use of network capacity 
		* TCP Reno 
		* TCP Cubic
* Delay\-based congestion control 
	* Reducing TCP\-induced latency
		* TCP Vegas 
		* TCP BBR
* Explicit congestion notification
* TCP is a complex, highly optimised, protocol 

#### QUIC Congestion Control

* The QUIC v1 standard adopts congestion control as used in TCP Reno 
* QUIC implementations tend to use Cubic or BBR congestion control in practice

#### Congestion Control Principles

* Key congestion control principles:
	* Packet loss as a congestion signal 
	* Conservation of packets in flight
	* Additive increase/multiplicative decrease
* Practical TCP congestion control: 
	* Robust IETF standards for TCP 
	* Embodies congestion control principles 
	* Extremely high performance

#### Key Principles: Packet Loss as a Congestion Signal

* Data flows from sender to receiver through a series of IP routers
* Routers perform two functions: 
	* Routing: receive packets, determine appropriate route to destination 
	* Forwarding: enqueue packets on outgoinglink for delivery
		* Queues shrink if packets are forwarded faster than they arrive  
		* Queues grow if packets arrive faster than they can be forwarded 
		* Queues have maximum size → packets discarded if the queue is full 
		* Congestion control can use this packet loss as a congestion signal

#### Key Principles: Conservation of Packets

* Acknowledgements returned by receiver
	* Send one packet for each acknowledgement received
	* Total number of packets in transit is constant
		* System is in equilibrium; queues neither increase nor decrease in size 
		* ACK clocking – each acknowledgement “clocks out” the next packet 
* Automatically reduces sending rate if network gets congested and delivers packets more slowly

#### Key Principles: AIMD Algorithms

* Sending rate follows additive increase, multiplicative decrease \(AIMD\) algorithm 
	* Start slowly, increase gradually to find equilibrium
		* Add a small amount to the sending speed each time interval without loss 
		* For a window-based algorithm w<sub>i</sub> = w<sub>i\-1</sub> \+ α each RTT, where α = 1 typically
	* Respond to congestion rapidly 
		* Multiply sending window by some factor β < 1 each interval loss seen
		* For a window\-based algorithm w<sub>i</sub> = w<sub>i-1</sub> × β each RTT, where β = 1/2 typically 
	* Faster reduction than increase → stability; TCP Reno

#### Congestion Control in TCP Reno

* TCP uses window\-based congestion control
	* Maintains a sliding window onto the available data that determines how much can be sent according to the AIMD algorithm
	* Plus slow start and congestion avoidance
	* Gives approximately equal share of the bandwidth to each flow sharing a link
* Basic congestion control algorithm known as TCP Reno

#### From Stop\-and\-Wait to Sliding Window Protocols

* Stop\-and\-wait protocols perform poorly
	* It takes time, t<sub>s</sub>, to send a packet
		* t<sub>s</sub> = \(packet size\) / \(link bandwidth\)
	* Acknowledgement returns t<sub>RTT</sub> seconds later
	* Link utilisation, U = t<sub>s</sub> / t<sub>RTT</sub>
		* Fraction of time link is sending packets → want U ≈ 1.0 
* Sliding window protocols improve on stop\-and\-wait by sending more than one packet before stopping for acknowledgement

#### Sliding Window Protocols Improve Link Utilisation

Sliding window protocols improve link utilisation using a congestion window – number of packets to be sent before an acknowledgement arrives.

Each returning acknowledgement for new data slides the window along, releasing next packet for transmission → if window sized correctly, each acknowledgement arrives just in time to release next packet.

What is the optimal size for the window? bandwidth × delay of path → **but neither is known to the sender**

#### TCP Reno Congestion Control

* TCP Reno is a sliding window protocol 
	* Optimised for not having information to know the correct window size 
* How to find the path capacity? 
	* Slow start to estimate the bottleneck link capacity
	* Congestion avoidance to probe for changes in capacity

#### TCP Reno: Choosing the Initial Window

* How to choose initial window size, W<sub>init</sub>? 
	* No information → need to measure path capacity
	* Start with a small window, increase until congestion 
	* W<sub>init</sub> = 1 packet per round\-trip time \(RTT\) is safe
		* Start at the slowest possible rate, equivalent to stop\-and\-wait, and increase
	* W<sub>init</sub> = 3 packets per RTT
		* Traditional TCP Reno approach 
	* W<sub>init</sub> = 10 packets per RTT
		* Modern TCP implementations
		* Compromise between safety and performance – measurements show this is generally safe at present 
		* Expect W<sub>init</sub> to gradually be increased as average network performance improves

#### TCP Reno: Finding the Path Capacity

* The initial window allows you to send something
	* Unlikely to be the optimal window size 
	* How to choose the correct window size to match the link capacity?
		* Slow start to rapidly find the correct window size for the path 
		* Congestion avoidance to adapt to changes in path capacity once connection is running

#### TCP Reno: Slow Start

* Assume W<sub>init</sub> = 1 packet per RTT – slow start to connection
	* It will be W<sub>init</sub> = 3 or W<sub>init</sub> = 10 in practice
* Rapidly increase window until network capacity is reached 
	* Each acknowledgement for new data increases congestion window, W, by 1 packet per RTT → congestion window doubles each RTT
	* If a packet is lost, halve congestion window back to previous value and exit slow start

* TCP Reno slow start phase:
	* Starts sending slowly 
	* Rapidly increases sending rate until a packet is lost
	* Resets sending rate to last known good rate when first loss occurs

#### TCP Reno: Congestion Avoidance

* After first packet is lost, TCP switches to congestion avoidance
	* The congestion window is now approximately the right size for the path
	* Goal is now to adapt to changes in network capacity
		* Perhaps the path capacity changes – radio signal strength changes for mobile device
		* Perhaps the other traffic changes – competing flows stop; additional cross\-traffic starts
	* Additive increase, multiplicative decrease of congestion window

* If a complete window of packets is sent without loss:
	* Increase congestion window by 1 packet per RTT, then send next window worth of packets 
	* Slow, linear, additive increase in window: W<sub>i</sub> = W<sub>i-1</sub> + 1

* If a packet is lost and detected via triple duplicate acknowledgement:
	* Transient congestion, but data still being received
	* Multiplicative decrease in window: W<sub>i</sub> = W<sub>i-1</sub> × 0.5
	* Rapid reduction in window allows congestion to clear quickly, avoids congestion collapse 
* Then, return to additive increase until next loss

* If a packet is lost and detected via timeout:
	* Either receiver or path has failed – reset to W<sub>init</sub> and re\-enter slow start
	* How long is the timeout? 
		* T<sub>rto</sub> = max\(1 second, average RTT + \(4 x RTT variance\)\)

#### Congestion Window Growth, Buffering, Throughput

* Bottleneck buffer size = bandwidth × delay
* Bottleneck queue never empty 
* Bottleneck link never becomes idle → sending rate varies, but receiver sees continuous flow 
* Congestion window follows a “sawtooth” pattern, but received rate is constant at approximately bottleneck bandwidth

#### TCP Reno: Summary

* TCP Reno is effective at keeping bottleneck link fully utilised 
	* Trades some extra delay to maintain throughput 
	* Provided sufficient buffering in the network: buffer size = bandwidth × delay 
	* Packets queued in buffer → delay 
* Limitations: 
	* Assumes packet loss is due to congestion; non-congestive loss, e.g., due to wireless interference, impacts throughput 
	* Congestion avoidance phase takes a long time to use increased capacity

#### TCP Performance on Fast Long\-distance Networks

* TCP Reno can perform poorly on fast long\-distance networks
	* e.g., multi\-gigabit per second inter\-continental links
	* Path with 10Gbps bandwidth and 100ms RTT requires congestion window \~100,000 packets 
	* In congestion avoidance, one packet lost and detected via triple duplicate ACK halves the window, then increase by 1 packet per RTT → 50,000 RTTs to recover sending rate 
		* Approximately 1.4 hours with 100ms RTT!

#### TCP Cubic

* TCP Cubic changes the congestion control algorithm 
	* During congestion avoidance, increases congestion window faster than TCP Reno on fast long\-distance networks
	* Rapidly increases congestion window after packet loss
	* Slows rate of increase as window approaches the largest successfully achieved window

#### TCP Cubic Congestion Control

* On packet loss during congestion avoidance, TCP Cubic reduces congestion window: W<sub>i</sub> = W<sub>i-1</sub> × 0.7
	* TCP Reno uses W<sub>i</sub> = W<sub>i-1</sub> × 0.5  
	* TCP Cubic is more aggressive
* After packet loss during congestion avoidance, TCP Cubic increases the congestion window as: W<sub>cubic</sub> = C\(t \- K\)<sup>3</sup> + W<sub>max</sub>
	* W<sub>max</sub> is the maximum window size reached before the loss 
	* t is the time since the packet loss
	* K is the time it will take to increase the window back to W<sub>max</sub>, assuming no further packet losses 
	* C = 0.4 is a constant that controls fairness to TCP Reno
* Many additional details included to ensure fairness with TCP Reno on slower, shorter\-RTT, networks

#### TCP Cubic vs Reno

* TCP Cubic is default in most modern operating systems
	* Much more complex than TCP Reno – core response is relatively straight\-forward 
	* Much complexity ensures fairness with TCP Reno in its typical operating regime; improves performance for networks with longer RTT and higher bandwidth
* Both algorithms use packet loss as congestion signal and eventually fill router buffers
	* Trade latency for throughput

#### Impact of TCP on Latency

* TCP Reno and TCP Cubic both aim to fill the network

* TCP Reno and Cubic use packet loss as congestion signal → increase congestion window until queue overflows and packet is lost
* No matter how much big the queue, TCP Reno or Cubic will cause it to overflow, if given enough data to send 
* Packets waiting in queues within network adds latency → increase RTT 

#### TCP Vegas: Reducing Latency

* Key insight: if sending faster than the network can deliver, packets will be queued 
	* TCP Reno and Cubic wait until the queue overflows and packets are lost before slowing down 
	* TCP Vegas watches for the increase in delay as the queue starts to fill up → slows down before the queue overflows 
		* Queues are smaller → lower latency
		* Packets are not lost, so don’t need retransmission
	* Only affects congestion avoidance; slow start unchanged

#### TCP Vegas Congestion Control

* Measure BaseRTT 
	* The smallest time between sending a packet and getting its acknowledgement 
	* BaseRTT will be from a packet delivered without much queueing
* Calculate ExpectedRate = W / BaseRTT
	* The congestion window, W, determines how many packets are sent each RTT 
	* If the network can support this sending rate, the complete window should be delivered within the RTT
* Measure ActualRate
	* Bytes sent divided by actual RTT, for each packet
	* Measure how fast packets are actually received, based on acknowledgements returned 
	* ActualRate ≤ ExpectedRate since packets can’t be delivered faster than they’re sent

* Compare ExpectedRate with ActualRate and adjust window:
	* If ExpectedRate \- ActualRate < R<sub>1</sub> then additive increase to window 
		* Data arriving at close to expected rate, can likely send faster 
	* If ExpectedRate - ActualRate \> R<sub>2</sub> then additive decrease to window
		* Data arriving slower than it’s being sent, slow down
	* Parameters R<sub>1</sub> and R<sub>2</sub>, where R<sub>1</sub> < R<sub>2</sub>, critical to performance

#### TCP Vegas: Limitations

* Delay\-based congestion control is a good idea in principle 
	* Reduces latency
	* Reduces packet loss 
* But loss\- and delay\-based congestion control don’t cooperate
	* TCP Reno and TCP Cubic aggressively increase queue sizes 
	* Increases RTT and reduces ActualRate as measured by TCP Vegas
	* Forces TCP Vegas to slow down; cycle repeats → TCP Vegas sending rate drops to zero over time 

* TCP Vegas is not used, because it can’t be deployed alongside TCP Reno or TCP Cubic

#### TCP BBR

* Is it possible to develop a delay-based congestion control algorithm for TCP that can be deployed on a network alongside TCP Reno and TCP Cubic? 
* Maybe – TCP BBR \(“Bottleneck Bandwidth & RTT”\) is one attempt 
	* Proposal from Google – measures RTT and bandwidth of the bottleneck link, directly sets congestion window 
	* Used by YouTube in some cases, but highly experimental
	* TCP BBR v2 in development, might solve these problems – this is an active research area

#### Explicit Congestion Notification

* TCP has inferred congestion through measurement
	* TCP Reno and Cubic → packets lost when queues overflow
		* Problematic because it increases delay
		* Problematic because of non\-congestive loss on wireless links 
* TCP Vegas → increase in delay as queues start to fill 
	* Conceptually a good idea, but difficult to deploy when competing with TCP Reno and Cubic 
* Why not have the network tell TCP congestion is occurring? 
	* Explicit Congestion Notification \(ECN\) field in IP header
	* Tell TCP to slow down if it’s overloading the network

#### ECN and IP

* Sender sets ECN bits on transmission:
	* 00 = Doesn’t support ECN, 01 = ECN capable
* If congestion occurs, congested router sets ECN bits to 11 \(“congestion experienced”\) 
	* Indicates that a queue of packets for some link is getting full, but has not yet overflowed – signal of congestion set by the network
	* If the queue overflows, packets are dropped 
* Cooperation between network and endpoints

#### ECN and TCP

* Receiver may get a TCP segment within an IP packet marked ECN Congestion Experienced \(ECN\-CE\) 
* ECN Echo \(ECE\) field in TCP header allow it to signal this back to the sender

* Sender reduces congestion window on receiving acknowledgement with ECE = 1 as if the packet had been lost
* Sets CWR = 1 in next packet to inform network and receiver it has done so

* ECN lets TCP react to congestion before packet loss occurs 
	* Routers signal congestion before queues overflow
	* Independent of choice of TCP congestion control algorithm 
	* Smaller queues → reduces latency, beneficial for video conferencing and gaming

* ECN extensions also exist in QUIC and RTP

#### ECN and TCP: Deployment

* TCP endpoints needed to be updated to support ECN → done 
	* Endpoints now support ECN and many now enable ECN by default 
		* ECN was widely implemented but disabled\-by\-default for many years, due to concerns that it wouldn’t pass through firewalls
		* Apple forced firewalls to be fixed: iOS 9 enabled ECN for 5% of connection;iOS 10 for 50%; iOS 11 and later for all connections 
* Most routers support ECN, relatively few enable it by default
	* Endpoints can react to ECN signals, but network is currently unlikely to provide them 
	* Starting to change – e.g., recent DOCSIS cable modems enable ECN
	* Will take time, but latency reduced as ECN is enabled throughout the network

#### Light Speed?

* Two factors impact latency for data transfer 
	* The time packets spend in queues within the network 
		* Impact of TCP congestion control algorithm
		* ECN to signal congestion before queues overflow
	* The time packets spend propagating down the links between routers
		* Speed at which light propagates through an optical fibre
		* Speed at which electrical signals propagate down a wire 
		* Speed at which radio signals propagate through the air

#### Reducing Propagation Delay

* Physically shorter links have lower propagation delay
	* Significant reduction in latency by laying new cables that follow great circle routes between popular destinations 
	* e.g., ocean floor cable from Japan to Europe via the north pole, rather than Pacific Ocean – US – Atlantic Ocean

* Signals propagate at the speed of light in the transmission medium
	* Speed of light in optical fibre \~200,000 km/s
	* Speed of light in vacuum 299,792 km/s 
* SpaceX Starlink deploying \~4,000 low earth orbit communications satellites 
	* \~47% reduction in latency since signals sent through vacuum rather than optical fibre
	*  With careful routing, satellite path can follow close to the most direct great circle route 

What application cares so much about reducing latency to spend $billions launching >4,000 satellites? Or new undersea cables? High frequency share trading.