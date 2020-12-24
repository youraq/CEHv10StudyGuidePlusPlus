# 10-DOS

### DoS \(Denial of Service\) Attacks

* Seeking to take down a system or deny access to it by authorized users
* **Botnet**: network of zombie computers a hacker uses to start a distributed attack
  * Can be controlled over HTTP, HTTPS, IRC, or ICQ

#### Basic Categories

* **Fragmentation Attack**: taking advantage of the system's ability to reconstruct fragmented packets
* **Volumetric Attack**: bandwidth attack, consuming all bandwidth for the system or service
* **Application Attack**
  * Consuming the resources necessary for the application to run
  * Application level attack is against weak code
  * Application attack is just the general term
* **TCP state-exhaustion Attack**: going after load balancers, firewalls and application servers by attacking connection state tables
* **SYN Flood**: sending thousands of SYN packets with fake source IP address and not responding to the SYN/ACK packets; lots of half connections where the 3-way hanndshake is never completed; eventually target runs out of resources
* **ICMP flood**: sending ICMP ECHO packets with a spoofed address; eventually reaches limit of packets per second sent
* **Smurf**: sending large number of pings to the broadcast address of the subnet with source IP spoofed as the target, entire subnet responds exhausting the target; using ICMP ECHO requests
* **Fraggle**: same as Smurf but with UDP packets
* **Ping of Death**: fragmenting ICMP messages, after reassembled, ICMP packet is larger than the maximum size and crashes the system
* **Teardrop**: overlapping numerous garbled TCP/IP fragments with oversized payloads, causes older systems to crash due to fragment reassembly
* **Phlashing**: also known as bricking a system, causing permanent damage to a system
* **LAND Attack** \(Local Area Network Denial\): sending a TCP SYN packet to the target with a spoofed IP the same as the target; if vulnerable, target loops endlessly and crashes
* **DDoS** \(Distributied Denial of Service\): incoming traffic flooding the victim originates from many different sources
* **DRDoS** \(Distributied Reflexion Denial of Service\): using IP spoofing, the source address is set to targeted victim, which means all the replies will go to the target and flood the target
* **Slowloris**: trying to keep many connections to the target web server open and hold them open as long as possible

#### Tools

* Low Orbit Ion Cannon \(LOIC\): DDoS tool that floods a target with TCP, UDP or HTTP requests
* Trinity: Linux based DDoS tool

