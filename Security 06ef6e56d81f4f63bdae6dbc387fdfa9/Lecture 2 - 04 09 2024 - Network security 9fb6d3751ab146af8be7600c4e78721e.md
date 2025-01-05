# Lecture 2 - 04.09.2024 - Network security

# The network stack

- Physical communication
- Point-to-point comm.
- Internetworking
- Transmission control
- The domain system name
- Hypertext transport protocol
- The OSI model

Alt ovenfor er designet uden at tænke på sikkerhed. 

Det skyldes, at man, da det blev designet, ikke tænkte at der ville komme et globalt internet, hvor man kan tilgå alt.

# Foundations of Networking

## Adversary capabilties (Dolev-Yao model)

Vores adversary har komplet kontrol over netværket. De kan:

- Intercepte beskeder
- genspille beskeder
- transformere beskeder
- indsætte beskeder
- slette beskeder.

## Adversary incapabilities

Vores adversary kan ikke gætte vores secrets.

Dvs. en Dolev-Yao adversary kan:

- Udgive sig for at være en bruger og sende beskeder i deres navn
- Intercepte beskeder
- Holde to brugere fra at kommunikere

Men kan ikke:

- Stjæle filer fra vores computer.

# Physical layer

**Responsibility:**

- Transmission af binær data over et fysisk link

**Interconnection via hub**

**Usually broadcast (e.g., IEEE 802.3 Ethernet)**

**Giver typisk ikke nogen garanti**

## Attacks on the physical layer

Eavesdropping (confidentiality):

- Frames are broadcast; I can see them even if they aren’t for me.

Tampering (integrity):

- You won’t detect my change

Denial-of-service (availability):

- If I put enough noise on the line, you won’t send or receive any messages

Message injection:

- I can put arbitrary messages on the wire

# Data-link layer

**Responsibility:**

- Regulerer hvordan vores computer tilgår det fysiske medium.
- Transmission of packets between hosts connected by a physical link.

**Solves addressing:**

- Media Access Control (MAC) addresses

**Solves (partly) reliability:**

- Checksums (e.g., IEEE 802.3 use of CRC)

**Performance gains by using switches rather than hubs**

## 802.3: Ethernet (frame)

![image.png](Lecture%202%20-%2004%2009%202024%20-%20Network%20security%209fb6d3751ab146af8be7600c4e78721e/image.png)

## Attacks on the data link layer

Tampering (integrity):

- CRC er kryptografisk svagt; 
Du kommer ikke til at fange ændringerne.
(Dette vil blive gjort i crypto-lektionen senere)

Message injection/MAC spoofing:

- Jeg kan putte arbitrere beskeder på ledningen
- Kan bruges til at udgive sig som en anden

Eavesdropping (confidentiality):

- Frames bliver broadcast;
Jeg kan se dem selv hvis de ikke er tiltænkt mig
- Switches: MAC flooding.

### MAC flooding

Transmit nok falske frames med nye src adresser til at switchens skema ikke længere holder nogle faktiske adresser.

- Nu bliver switchen nødt til at broadcaste alle frames til alle modtagere.

![image.png](Lecture%202%20-%2004%2009%202024%20-%20Network%20security%209fb6d3751ab146af8be7600c4e78721e/image%201.png)

# Network layer

Tager sig af at sende beskeder fra den ene side af verden til den anden. 

- Dvs. beskeder vi ikke fysisk selv kan sende, sørge network laget for at route frem til destinationen.

**IP protocol**

- IPv4
- Nu til dags kan du ikke lave en ny IPv4 adresse, da alle adresser er optaget. Derfor rykker vi til IPv6 nu til dags.

**Hosts identificeres med IP adresser**

**Best-effort (unreliable) delivery**

- Der er ingen garanti i IP-protokollen for at vores beskeder rent faktisk kommer frem

**Kan introducere packet duplikation, out-of-order delivery**

- Hvis du sender 4 beskeder kan det f.eks. være at besked 3 tager en langsom rute og besked 4 tager en hurtig og derfor ankommer før besked 3.

## IP operations

- Next-hop routing
- BGP, ARP (lader os finde andre IP adresser på netværket), DHCP (automatisk tildeling af IP på netværk)
- MTU (v4 only), Fragmentation

## IPv4 Header

![image.png](Lecture%202%20-%2004%2009%202024%20-%20Network%20security%209fb6d3751ab146af8be7600c4e78721e/image%202.png)

## Spoofing

ARP Cache Poisoning (?)

- aka ARP spoofing, ARP Poison Routing
- Spoof ARP “er” packets der redirecter trafik der er tiltænkt en anden IP til min maskine

IP Spoofing

- DOS angreb. (Overload victim)

DHCP Starvation

- Få DHCP servicen til ikke at fungere

### IP Spoofing

![image.png](Lecture%202%20-%2004%2009%202024%20-%20Network%20security%209fb6d3751ab146af8be7600c4e78721e/image%203.png)

### Local denial-of-service attacks

- ARP Cache poisoning
- DHCP Starvation

### Remote denial-of-service attacks

- Ping flooding
- IP fragmentation attack
- Distributer angrebet til mange angribende maskiner for maximum effekt

# Transport layer

## TCP

- Connection-orienteret, reliable, streaming protokol
- Opnået med besked/acknowledgment sekvens numre, timeouts.
- Protoko specificeret som en rimelig kompleks state machine
- Også: Flow kontrol, congestion control

## Connection  setup

![image.png](Lecture%202%20-%2004%2009%202024%20-%20Network%20security%209fb6d3751ab146af8be7600c4e78721e/image%204.png)

![image.png](Lecture%202%20-%2004%2009%202024%20-%20Network%20security%209fb6d3751ab146af8be7600c4e78721e/image%205.png)

## TCP sequence prediction attack

- Suppose we want to ji-jack a connection from host A to B
- TCP Sequence numbers are sent in cleartext (eavesdropping)
- Liste to traffic from B. Kill B’s end of the connection
- Spoof TCP packets to A

## TCP RESET attack

- Spoof TCP packet with RST set to 1.
- Remote system should drop connection
- Bypassing IDS/Firewall may require sequence prediction

## TCP SYN flood

![image.png](Lecture%202%20-%2004%2009%202024%20-%20Network%20security%209fb6d3751ab146af8be7600c4e78721e/image%206.png)

# Application layer

## Domain names

- Hvordan finder jeg IP adressen for www.itu.dk?
- Ved brug a UDP query til domæne-navn systemet
- Premis: Du skal kende *en* name-/DNS server

## Attacks on GTP, Telnet

- Login credentials sendt i cleartext
- Adversary kan få brugernavn og kodeord bare ved at eavesdroppe.
- *der var et 3. punkt jeg ikke fik skrevet ned ups.*

# All layers

![image.png](Lecture%202%20-%2004%2009%202024%20-%20Network%20security%209fb6d3751ab146af8be7600c4e78721e/image%207.png)

# Denial of Service

> “What happens if this botnet actually takes down [google.com](http://google.com) and we lose all of our revenue?”
- Google
> 

## Consume the resources of your computer

- Network bandwidth
- System resources
- Application resources

## Ping flood

![image.png](Lecture%202%20-%2004%2009%202024%20-%20Network%20security%209fb6d3751ab146af8be7600c4e78721e/image%208.png)

## Source address spoofing

![image.png](Lecture%202%20-%2004%2009%202024%20-%20Network%20security%209fb6d3751ab146af8be7600c4e78721e/image%209.png)

## UDP flood

- Samme idé som ping flood, me UDP
- Rettet mod specifikke porte
- Målet returnere UDP-svar eller ICMP besked
- Forbruger både bandwidth og lokale ressourcer.

## SYN spoofing

![image.png](Lecture%202%20-%2004%2009%202024%20-%20Network%20security%209fb6d3751ab146af8be7600c4e78721e/image%2010.png)

## HTTP attacks

Flood, Spidering,

Slow loris: Multiple HTTP requests. Don’t terminate requests. Add new headers once in a while.

## Distributed Denial of Service attacks

- Hack en masse andre devices (zombies)
- Giv dem instrukser (botnet) til at DDoS dit faktiske mål
- Arranger zombies i et hierarki. IRC populært for command-and-control (C&C)

## Amplification attacks

- Generer mere end et svar for hver spoofed request
- DNS request “any”: 30 bytes
- DNS response to “any”: 150 bytes
- Amplification factor: 5x

![image.png](Lecture%202%20-%2004%2009%202024%20-%20Network%20security%209fb6d3751ab146af8be7600c4e78721e/image%2011.png)

The amount of data you can generate in DOS attacks is increasing all the time: 

![image.png](Lecture%202%20-%2004%2009%202024%20-%20Network%20security%209fb6d3751ab146af8be7600c4e78721e/image%2012.png)

## Defenses

- Cannot be prevented completely: 
Legitimate traffic; the Slashdot effect
- DNS reflection:
Firewall may block replies to requests I didn’t send
- Amplification via IP broadcast:
Firewall blocks broadcasts from outside local network

- RFC 2827. Block IP-spoofing at earliest point - local ISP knows if originator IP is legit or not.
- SYN-cookies vs SYN-spoofing: encode all necessary state in SYN-ACK sequence number(!)
- Vs. Application-resources: CAPTCHAs

# Firewalls and IDS (Intrusion Detection Systems)

## Firewall

Selectively block or reroute network traffic.

The adversary can’t attack me if he cannot send me network packets!

Firewall should by default deny everything, and then slowly open up only the services you are interested in using.

### Packet filtering firewall

- Filter based on packet contents:
src/tgt IP, src/tgt port number, tcp/ip flags, interface, …
- Default: discard or forward

![image.png](Lecture%202%20-%2004%2009%202024%20-%20Network%20security%209fb6d3751ab146af8be7600c4e78721e/image%2013.png)

### Stateful packet inspection firewalls

- Keeps state, typically TCP connections.
- Stateless must allow connection on >1023 ports in general

![image.png](Lecture%202%20-%2004%2009%202024%20-%20Network%20security%209fb6d3751ab146af8be7600c4e78721e/image%2014.png)

### More on firewalls

- Other types: Application-level, Circuit-level
- Location is important:
Read on your own: Stallings 9.4, 9.5

## Intrusion Detection Systems (IDS)

- Detect potentially malicious activity by analysing network traffic
- Location: network or host
- Detection strategies: signature-based (detect known attack patterns), anomaly/specification-based (flag network activity that deviates from normal traffic)