# Session Hijacking



### Session Hijacking

* Attacker waits for a session to begin and after the victim authenticates, steals the session for himself
* Predicting can be done by knowing the window size and the packet sequence number
* Also can be done via brute force, calculation or stealing

#### Steps

1. Sniff the traffic between the client and server
2. Monitor the traffic and predict the sequence numbering
3. Desynchronize the session with the client
4. Predict the session token and take over the session
5. Inject packets to the target server

#### Countermeasures

* Using unpredictable session IDs
* Limiting incoming connections
* Minimizing remote access
* Regenerating the session key after authentication
* Using **IPsec** to encrypt

#### IPsec \(Internet Protocol Security\)

* **Transport Mode**
  * Payload and ESP trailer are encrypted, not IP header
  * Can be used in NAT because the original packet is still routed in exactly the same manner as it would have been without IPsec
* **Tunnel mode**
  * Everything is encrypted
  * Cannot be used with NAT
* **Architecture Protocols**
  * **Authentication Header**: guarantying the integrity and authentication of IP packet sender
  * **Encapsulating Security Payload** \(ESP\): providing origin authenticity and integrity as well as confidentiality
  * **Internet Key Exchange** \(IKE\): producing the keys for the encryption/decryption process, port 500
  * **Oakley**: using Diffie-Hellman to create master and session keys
  * **Internet Security Association Key Management Protocol** \(ISAKMP\): software that facilitates encrypted communication between two endpoints

#### Tools

* **Ettercap**: man-in-the-middle tool and packet sniffer on steroids
* **Zaproxy**
* **Paros proxy**
* **Burp Suite**
* **Hamster**
* **IKE-scan**: IPsec VPN scanning and fingerprinting tool

