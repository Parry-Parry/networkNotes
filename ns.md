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