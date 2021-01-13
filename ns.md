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
- The maximum bitrate of a channel is described by Nyquist’s theorem: R<sub>max</sub> $\leq$ 2B log<sub>2</sub>V
