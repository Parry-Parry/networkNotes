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
- The maximum bitrate of a channel is described by Nyquist’s theorem: R<sub>max</sub> \le 2Blog<sub>2</sub>V
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
