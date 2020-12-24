# 04-Enumeration

## Table of Contents

* [Enumeration](04_enumeration.md#enumeration)
  * [NetBIOS \(Network Basic Input/Output System\) Enumeration](04_enumeration.md#netbios-network-basic-input-output-system-enumeration)
    * [NetBIOS code and meaning](04_enumeration.md#netbios-network-basic-input-output-system-enumeration)
  * [SNMP \(Simple Network Management Protocol\) Enumeration](04_enumeration.md#snmp-simple-network-management-protocol-enumeration)
  * [SMTP \(Simple Mail Transfer Protocol\) Enumeration](04_enumeration.md#smtp-simple-mail-transfer-protocol-enumeration)
  * [NTP \(Network Time Protocol\) Enumeration](04_enumeration.md#ntp-network-time-protocol-enumeration)
  * [LDAP \(Lightweight Directory Access Protocol\) Enumeration](04_enumeration.md#ldap-lightweight-directory-access-protocol-enumeration)
  * [NFS \(Network File System\) Enumeration](04_enumeration.md#nfs-network-file-system-enumeration)
  * [SMB \(Server Message Block\) Enumeration](04_enumeration.md#smb-server-message-block-enumeration)



### Enumeration

* Listing the items that are found within a specific target
* Always active by nature

#### NetBIOS \(Network Basic Input/Output System\) Enumeration

* NetBIOS provides name servicing, connectionless communication and some Session layer stuff
* NetBIOS is the browser service in Windows designed to host information about all machines within domain or TCP/IP network segment
* NetBIOS name is a **16-character ASCII string** used to identify devices Of those 16 characters, 15 are used for the device name, and the remaining character is reserved for the service name or name record type
* NetBIOS name resolution doesn't work on IPv6
* nbtstat \(on Windows\)
  * Local table: `nbtstat -n`
  * Remote information: `nbtstat -A <IPADDRESS>`
  * Cache information: `netstat -c`
* Other Tools
  * SuperScan
  * Hyena
  * NetBIOS Enumerator
  * NSAuditor

**NetBIOS code and meaning**

| Code | Type | Meaning |
| :--- | :--- | :--- |
|  | UNIQUE | Hostname |
|  | GROUP | Domain name |
|  | UNIQUE | Windows Messenger service |
|  | UNIQUE | Domain master browser |
|  | GROUP | Domain controller |
|  | UNIQUE | Master browser for subnet |
|  | UNIQUE | File Service |

#### SNMP \(Simple Network Management Protocol\) Enumeration

* Used for network device management and uses both an agent and a manager to ensure logging and control
  * Agents are embedded in every network device
  * Manager is installed on a separate computer
* There is a read-only and a read-write version
  * Default read-only string is **public**
  * Default read-write string is **private**
* SNMP uses **community strings** which function as passwords, sent in cleartext unless using SNMP v3
* **Management Information Base** \(MIB\): database that stores information, it uses ASN.1 \(Abstract Syntax Notation One\)
* **Object Identifiers** \(OID\): identifiers for information stored in MIB
* **SNMP GET**: getting information about the system
* **SNMP SET**: setting information about the system
* **Types of objects**
  * **Scalar**: single object
  * **Tabular**: multiple related objects that can be grouped together
* Tools
  * Engineer's Toolset
  * SNMPScanner
  * OpUtils 5: includes SNMP tools
  * SNScan

#### SMTP \(Simple Mail Transfer Protocol\) Enumeration

* VRFY: verifying email addresses; code 200 success, code 550 failure
* EXPN: providing actual delivery address of mailing list and aliases
* RCPT TO: defining recipients

#### NTP \(Network Time Protocol\) Enumeration

* Querying can give you list of systems connected to the server name and IP
* Tools
  * NTP Server Scanner
  * AtomSync
* Commands
  * ntptrace
  * ntpdc
  * ntpq

#### LDAP \(Lightweight Directory Access Protocol\) Enumeration

* Connecting on 389 to a Directory System Agent \(DSA\)
* Returning information such as valid user names, domain information, addresses, telephone numbers, system data, organization structure and other items, interface with Active Directory \(AD\)
* Tools
  * Softerra
  * JXplorer
  * Lex \(The LDAP Explorer\)
  * LDAP Admin Tool

#### NFS \(Network File System\) Enumeration

*  NFS  is a protocol allowing remote access to a filesystem through the network. All Unix systems can work with this protocol.
* Port 111 and 2049
* showmount -e &lt;IPaddress&gt;
  * Show the accessible NFS shares

#### SMB \(Server Message Block\) Enumeration

* Tools :
  * smbclient
  * smbmap

