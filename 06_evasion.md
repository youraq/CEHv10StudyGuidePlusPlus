# 06-Evasion

## Table of Contents

* [Evasion](06_evasion.md#evasion)
  * [IDS \(Intrusion Detection System\)](06_evasion.md#ids-intrusion-detection-system)
    * [Types of IDS](06_evasion.md#ids-intrusion-detection-system)
    * [Types of Alerts](06_evasion.md#ids-intrusion-detection-system)
  * [IPS \(Intrusion Prevention System\)](06_evasion.md#ips-intrusion-prevention-system)
    * [Types of IPS](06_evasion.md#ips-intrusion-prevention-system)
  * [Firewall](06_evasion.md#firewall)
    * [Firewall Technologies](06_evasion.md#ips-intrusion-prevention-system)
    * [Types of Firewall](06_evasion.md#firewall)
  * [Honeypot](06_evasion.md#honeypot)
  * [Evasion Techniques](06_evasion.md#evasion-techniques)
    * [Firewall Evasion](06_evasion.md#evasion-techniques)



### Evasion

#### IDS \(Intrusion Detection System\)

* Hardware or software devices that examine streams of packets for malicious behavior

**Types of IDS**

* **Signature based**: comparing packets against a list of known traffic patterns
* **Anomaly based**: making decisions on alerts based on learned behavior and "normal" patterns
* **HIDS** \(Host-based intrusion detection system\): examining specific host-based actions, such as what applications are being used, what files are being accessed and what information resides in the kernel logs
* **NIDS** \(Network-based intrusion detection system\): scanning network traffic, do not use host system resources
* **NBA** \(Network behavior analysis\): examining network traffic to identify threats that generate unusual traffic flows
* **Snort**: a widely deployed IDS that is open source
  * Runs in three different modes
    * **Sniffer Mode**: watching packets in real time
    * **Packet Logger Mode**: saving packets to disk for review at a later time
    * **NIDS Mode**: analyzing network traffic against various rule sets
  * Syntax
    * Alert about traffic coming not from an external network to the internal one on port 31337:

      ```text
      alert tcp !HOME_NET any -> $HOME_NET 31337 (msg : "BACKDOOR ATTEMPT-Backorifice")
      ```

    * Example output:

      ```text
      10/19-14:48:38.543734 0:48:542:2A:67 -> 0:10:B5:3C:34:C4 type:0x800 len:0x5EA
      **xxx -> xxx TCP TTL:64 TOS:0x0 ID:18112 IpLen:20 DgmLen:1500 DF**
      ```

**Types of Alerts**

* **True Positive** \(Attack - Alert\): activity was an attack, IDS identifies as an attack
* **False Positive** \(No Attack - Alert\): activity was acceptable, but IDS identifies as an attack
* **False Negative** \(Attack - No Alert\): activity was an attack, but IDS identifies as an acceptable behavior
* **True Negative** \(No Attack - No Alert\): activity was acceptable, IDS identifies as an acceptable behavior

#### IPS \(Intrusion Prevention System\)

* Identifying malicious activity, logs information about this activity, reports it and attempts to block or stops it

**Types of IPS**

* **NIPS** \(Network-based intrusion prevention system\): monitoring the entire network for suspicious traffic by analyzing protocol activity
* **HIPS** \(Host-based intrusion prevention system\): an installed software package which monitors a single host for suspicious activity by analyzing events occurring within that host
* **WIPS** \(Wireless intrusion prevention system\): monitoring a wireless network for suspicious traffic by analyzing wireless networking protocols

#### Firewall

* An appliance within a network protects internal resources from unauthorized access
* Only uses rules that **implicitly denies** traffic unless it is allowed
* Often uses **network address translation** \(NAT\) which can apply a one-to-one or one-to-many relationship between external and internal IP addresses
* **Bastion Host**: hosts on the screened subnet designed to protect internal resources, using the concept "separation of duties"
* **Screened Subnet**: DMZ, hosts all public-facing servers and services
* **Private zone**: hosts internal hosts that only respond to requests from within that zone
* **Multi-homed**: firewall that has 2 or more interfaces

```text
- Single Homed Network:

  Enterprice ---------- ISP

- Dual Homed Network:

  Enterprice ========== ISP

- Single Multi-homed Network

             ---------- ISP1
  Enterprice
             ---------- ISP2

- Dual Multi-homed Network

             ========== ISP1
  Enterprice
             ========== ISP2
```

**Firewall Technologies**

| OSI | Firewall Technology |
| :--- | :--- |
| 7 | VPN, Application Proxies |
| 6 | VPN |
| 5 | VPN, Circuit-level Gateway |
| 4 | VPN, Packet Filtering |
| 3 | VPN, NAT, Packet Filtering, Stateful Multilayer Inspection |
| 2 | VPN, Packet Filtering |
| 1 | Not Applicable |

**Types of Firewall**

* **Packet-filtering**: only looking at packet headers \(IP address, packet type and port number\), layer 3 Network
* **Circuit-level gateway**: checking TCP handshake, does not filer individual packets, firewall that works on layer 5 Session
* **Application-level gateway**: working like a proxy, allowing specific services in and out, WAF, layer 7 Application
* **Stateful inspection**: combining above 3 types of firewalls, dynamic packet filtering, firewalls that track the entire status of a connection

#### Honeypot

* A system setup as a decoy to entice attackers, to research attack methodologies
* Should not include too many open services or look too easy to attack
* **High interaction**: actually running all services and applications and is designed to be completely compromised
* **Medium interaction**: simulating a real OS, applications and its services
* **Low interaction**: simulating a number of services and cannot be completely compromised
* Examples
  * Specter
  * Honeyd
  * KFSensor

#### Evasion Techniques

* **Fragmentation**: splitting up packets so that the IDS can't detect the real intent, `nmap -f`
* **Time-To-Live Attack** \(TTL\)
  * Each router along a data path decrements TTL by 1
  * TTL reaches 0, package is dropped
  * Attacker has a prior knowledge of topology of target network, in order to calculate TTL
  * Breaking traffic to fragments, eg: Frag 1, Frag 2, Frag 3
  * Sending fragments as below as an exmaple:

    ```text
    Attacker          NIDS             Router    Victim
    Frag 1        ->  Frag 1            ->       Frag 1
    Frag 2, TTL=1 ->  Frag 1, 2        Dropped   Frag 1, Waiting 2
    Frag 3        ->  Frag 1, 2, 3      ->       Frag 1, 3 Waiting 2
                    False Reassembly
    Real Frag 2   ->  Frag 2            ->       Frag 1, 2, 3, Correct Reassembly
    ```
* **Slow down**: faster scanning such as using nmap's -T5 switch will get you caught. Pros use -T1 switch to get better results
* **Unicode encoding**: working with web requests - using Unicode characters instead of ascii can sometimes get past
* **Network flooding**: triggering alerts that aren't your intended attack so that confuses firewalls/IDS and network admins
* **Insertion Attack**: confusing IDS by forcing it to read invalid packets
* **Spoofing**: can only be used when you don't expect a response back to your machine
* **Source routing**: specifying the path a packet should take on the network; most systems don't allow this anymore
* **IP Address Decoy**: sending packets from your IP as well as multiple other decoys to confuse the IDS/Firewall as to where the attack is really coming from
  * `nmap -D RND:10 x.x.x.x`
  * `nmap -D decoyIP1,decoyIP2....,sourceIP,.... [target]`
* **Proxy**
  * Hiding true identity by filtering through another computer
  * Also can be used for other purposes such as content blocking evasion, etc
  * **Proxy chains**: chains multiple proxies together
    * Proxy Switcher
    * Proxy Workbench
    * ProxyChains
* **Tor**
  * A specific type of proxy that uses multiple hops to a destination
  * Endpoints are peer computers
* **Anonymizers**: hiding identity on HTTP traffic \(port 80\)
* Tools
  * Nessus: also a vulnerability scanner
  * ADMutate: creating scripts not recognizable by signature files
  * Whisker: session Splicing

**Firewall Evasion**

* **Firewalking**: going through every port on a firewall to determine what is open
* Firewall type can be discerned by banner grabbing
* The best way around a firewall will always be a compromised internal machine
* **HTTP tunneling**: crafting port 80 segments to carry a payload for protocols the firewall may have, then on other end \(internal machine\) to pull the payload out of all those 80 packets

