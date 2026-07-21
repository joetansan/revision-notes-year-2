# Enterprise Network Security — Written Test 2 PRACTICE TEST
## Topics: Week 5–13 | Duration: 1 hour 15 minutes
## Format: MCQ, True/False, Multi-Select, Match-the-Following, Fill-in-the-Blanks, Open-Ended

---

# SECTION A: Multiple Choice Questions (MCQ)

**Instructions:** Choose the BEST answer for each question.

**Q1.** What is the default administrative distance of OSPF?
- A) 120
- B) 90
- C) 100
- D) 110

**Answer: D**

---

**Q2.** Which of the following OSPF packet types is used to discover neighbours and establish adjacencies?
- A) LSAck
- B) Hello
- C) LSU
- D) DBD

**Answer: B**

---

**Q3.** Which IPsec protocol provides BOTH authentication and encryption?
- A) IKE
- B) AH
- C) GRE
- D) ESP

**Answer: D**

---

**Q4.** What is the wildcard mask for the network 172.16.0.0/16?
- A) 0.0.255.255
- B) 0.0.0.255
- C) 255.255.0.0
- D) 255.255.255.0

**Answer: A**

---

**Q5.** Which type of firewall maintains a state table to track active connections?
- A) Application firewall
- B) Packet filtering firewall
- C) Web application firewall
- D) Stateful packet inspection firewall

**Answer: D**

---

**Q6.** Which of the following is a disadvantage of NAT?
- A) It hides internal IP addresses
- B) It conserves public IPv4 addresses
- C) It increases forwarding delays
- D) It provides address multiplexing

**Answer: C**

---

**Q7.** Which Bluetooth attack involves accessing unauthorized information and stealing data stored on a device?
- A) Blueborne
- B) Bluebugging
- C) Bluesnarfing
- D) Bluejacking

**Answer: C**

---

**Q8.** Which IPS alarm type is the MOST dangerous?
- A) False Negative
- B) True Positive
- C) True Negative
- D) False Positive

**Answer: A**

---

**Q9.** Which command enables OSPF MD5 authentication on an interface?
- A) `area 0 authentication`
- B) `ip ospf authentication message-digest`
- C) `ip ospf authentication`
- D) `service password-encryption`

**Answer: B**

---

**Q10.** In which IKE phase are IPsec SA parameters negotiated?
- A) Both phases simultaneously
- B) IKE Phase 1
- C) IKE Phase 2
- D) IKE Phase 3

**Answer: C**

---

**Q11.** Which of the following is the correct number range for extended IP ACLs?
- A) 100–199
- B) 1–99
- C) 1000–1099
- D) 200–299

**Answer: A**

---

**Q12.** What does the `established` keyword in an extended ACL check for?
- A) The ACK flag is set
- B) The SYN flag is set
- C) The RST flag is set
- D) The FIN flag is set

**Answer: A**

---

**Q13.** Which NAT type maps multiple private IP addresses to a single public IP using port numbers?
- A) Dynamic NAT
- B) PAT (NAT Overload)
- C) Proxy NAT
- D) Static NAT

**Answer: B**

---

**Q14.** Which wireless security protocol uses AES encryption and is the strongest?
- A) WPA2
- B) WEP
- C) WPA3
- D) WPA

**Answer: A**

---

**Q15.** What is the purpose of the Diffie-Hellman exchange in IPsec?
- A) To define interesting traffic
- B) To authenticate users
- C) To securely exchange cryptographic keys
- D) To encrypt data traffic

**Answer: C**

---

**Q16.** Which of the following describes an IDS?
- A) A device that only filters packets based on headers
- B) An active device that blocks malicious traffic inline
- C) A device that performs NAT translations
- D) A passive device that monitors copies of traffic and generates alerts

**Answer: D**

---

**Q17.** Which OSPF authentication type sends the password in plaintext?
- A) MD5 authentication
- B) SHA authentication
- C) Simple password authentication
- D) Null authentication

**Answer: C**

---

**Q18.** Which of the following is NOT a zone in a typical firewall architecture?
- A) Quarantine zone
- B) Semi-trusted zone (DMZ)
- C) Trusted zone
- D) Untrusted zone

**Answer: A**

---

**Q19.** What does the `retired true` command do in IPS signature configuration?
- A) Disables the IPS entirely
- B) Stops the signature from being compiled into memory
- C) Deletes the signature permanently
- D) Removes the signature from the signature file

**Answer: B**

---

**Q20.** Which protocol number does ESP use?
- A) 51
- B) 47
- C) 500
- D) 50

**Answer: D**

---

# SECTION B: True or False

**Instructions:** Write TRUE or FALSE for each statement.

**Q21.** OSPF is a classful routing protocol.
**Answer: FALSE** — OSPF is classless (sends subnet mask info).

---

**Q22.** Standard ACLs should be placed closest to the source of traffic.
**Answer: FALSE** — Standard ACLs should be placed closest to the destination.

---

**Q23.** The implicit "deny any" at the end of every ACL is visible in the configuration.
**Answer: FALSE** — It is invisible/implicit but always present.

---

**Q24.** ESP operates on IP protocol number 50.
**Answer: TRUE**

---

**Q25.** PAT uses source port numbers to distinguish between sessions from different internal hosts.
**Answer: TRUE**

---

**Q26.** An IPS sensor in promiscuous mode can stop attacks before they reach the target.
**Answer: FALSE** — Promiscuous mode is IDS (passive, alerts only). IPS inline mode can stop attacks.

---

**Q27.** WEP uses the RC4 encryption algorithm.
**Answer: TRUE**

---

**Q28.** OSPF MD5 authentication encrypts the actual data traffic between routers.
**Answer: FALSE** — OSPF authentication only authenticates routing updates, it does NOT encrypt data traffic.

---

**Q29.** A composite IPS signature requires state information and can span multiple packets.
**Answer: TRUE**

---

**Q30.** The `service password-encryption` command encrypts OSPF routing updates.
**Answer: FALSE** — It only encrypts passwords displayed in the running configuration file.

---

# SECTION C: Multi-Select Questions

**Instructions:** Choose ALL correct answers.

**Q31.** Which three parameters must match for two OSPF routers to become neighbours? (Choose three.)
- A) Hello interval
- B) Process ID
- C) Dead interval
- D) Network type
- E) Router ID

**Answer: A, C, D**

---

**Q32.** Which two services does ESP provide? (Choose two.)
- A) Confidentiality (encryption)
- B) Routing
- C) Authentication and integrity
- D) NAT translation
- E) DHCP

**Answer: A, C**

---

**Q33.** Which two are characteristics of NGFWs? (Choose two.)
- A) Application awareness
- B) Only works at Layer 3
- C) Identity awareness
- D) Cannot inspect encrypted traffic
- E) No integration with IPS

**Answer: A, C**

---

**Q34.** Which two commands are required to enable IPS SDEE message logging? (Choose two.)
- A) `logging on`
- B) `ip ips notify log`
- C) `ip http server`
- D) `ip ips notify sdee`
- E) `ip sdee events 500`

**Answer: C, D**

---

**Q35.** Which are private IP address ranges according to RFC 1918? (Choose three.)
- A) 10.0.0.0 – 10.255.255.255
- B) 11.0.0.0 – 11.255.255.255
- C) 172.16.0.0 – 172.31.255.255
- D) 192.168.0.0 – 192.168.255.255
- E) 169.254.0.0 – 169.254.255.255

**Answer: A, C, D**

---

# SECTION D: Match the Following

**Q36.** Match each OSPF packet type to its function.

| # | Packet Type | | Function |
|---|-------------|---|----------|
| 1 | Hello | ___ | A) Confirm receipt of LSU |
| 2 | DBD | ___ | B) Request more info about a DBD entry |
| 3 | LSR | ___ | C) Discover neighbours, maintain adjacency |
| 4 | LSU | ___ | D) Abbreviated list of link-state database |
| 5 | LSAck | ___ | E) Carries link-state information |

**Answer: 1-C, 2-D, 3-B, 4-E, 5-A**

---

**Q37.** Match each IPS alarm type to its description.

| # | Alarm Type | | Description |
|---|------------|---|-------------|
| 1 | True Positive | ___ | A) Alarm generated for normal user traffic |
| 2 | False Positive | ___ | B) No alarm generated for attack traffic |
| 3 | True Negative | ___ | C) Alarm generated for attack traffic |
| 4 | False Negative | ___ | D) No alarm generated for normal user traffic |

**Answer: 1-C, 2-A, 3-D, 4-B**

---

**Q38.** Match each wireless attack to its description.

| # | Attack | | Description |
|---|--------|---|-------------|
| 1 | Evil Twin | ___ | A) Sending unsolicited messages to Bluetooth devices |
| 2 | Rogue AP | ___ | B) Mimics a legitimate AP so users connect to it |
| 3 | Bluejacking | ___ | C) Unauthorized AP installed on a secure network |
| 4 | Bluesnarfing | ___ | D) Stealing data from a Bluetooth device |

**Answer: 1-B, 2-C, 3-A, 4-D**

---

**Q39.** Match each firewall type to the OSI layer(s) it operates on.

| # | Firewall Type | | OSI Layer(s) |
|---|---------------|---|-------------|
| 1 | Packet Filtering | ___ | A) Layers 3, 4, 5, 7 |
| 2 | Stateful Inspection | ___ | B) Layer 3 (sometimes 4) |
| 3 | Application Firewall | ___ | C) Layers 3–4 |

**Answer: 1-B, 2-C, 3-A**

---

**Q40.** Match each NAT term to its description.

| # | Term | | Description |
|---|------|---|-------------|
| 1 | Inside Local | ___ | A) Address of source as seen from outside network |
| 2 | Inside Global | ___ | B) Address of destination as seen from outside |
| 3 | Outside Global | ___ | C) Address of source as seen from inside (private) |
| 4 | Outside Local | ___ | D) Address of destination as seen from inside |

**Answer: 1-C, 2-A, 3-B, 4-D**

---

# SECTION E: Fill in the Blanks

**Q41.** OSPF uses a default Administrative Distance of _______.
**Answer: 110**

---

**Q42.** The three parameters that must match for OSPF neighbours are: _______, _______, and _______.
**Answer: Hello interval, Dead interval, Network type**

---

**Q43.** An ACL is a sequential series of _______ that tell the router what packets to accept or _______.
**Answer: filters/statements, deny/drop**

---

**Q44.** The IPsec protocol that provides authentication and integrity but NOT encryption is called _______.
**Answer: AH (Authentication Header)**

---

**Q45.** The process of translating multiple private IP addresses to a single public IP using port numbers is called _______ or _______.
**Answer: PAT (Port Address Translation), NAT Overload**

---

**Q46.** WEP's Initialization Vector (IV) is only _______ bits long, which creates approximately _______ possible values.
**Answer: 24, 16 million (2^24)**

---

**Q47.** An IPS signature that consists of a single packet and requires no state information is called an _______ signature.
**Answer: Atomic**

---

**Q48.** The command _______ is used to apply a standard ACL to an interface, while _______ is used to restrict VTY access.
**Answer: ip access-group, access-class**

---

**Q49.** In IKE, Phase 1 authenticates peers and establishes a secure channel, while Phase 2 negotiates _______ parameters.
**Answer: IPsec SA (Security Association)**

---

**Q50.** A _______ positive alarm occurs when the IPS generates an alarm for normal user traffic that should not have triggered an alarm.
**Answer: False**

---

# SECTION F: Open-Ended Questions

**Q51.** Explain the difference between Standard ACLs and Extended ACLs. Include number ranges, what they can filter on, and recommended placement.

**Model Answer:**
Standard ACLs (numbered 1–99) can only filter on the **source IP address**. They should be placed **closest to the destination** because they can't distinguish between different destinations — placing them near the source would block all traffic from that host.

Extended ACLs (numbered 100–199) can filter on **source IP, destination IP, protocol (TCP/UDP/ICMP), and port numbers**. They should be placed **closest to the source** because they can precisely match on destination, and filtering early saves bandwidth by dropping unwanted traffic before it traverses the network.

Both types have an implicit "deny any" at the end and must be applied to an interface using `ip access-group`.

---

**Q52.** Describe the three types of NAT (Static, Dynamic, PAT). For each, explain how it works, when you would use it, and give an example.

**Model Answer:**

**Static NAT:** One-to-one permanent mapping between a private IP and a public IP. The mapping never changes. Use for devices that need a consistent public address accessible from the Internet, such as web servers. Example: 192.168.1.10 is always mapped to 209.165.200.225.

**Dynamic NAT:** Many-to-many mapping from a pool of public IPs. When an inside device needs Internet access, it grabs an available public IP from the pool on a first-come, first-served basis. Use when you have more public IPs than simultaneous users. Example: A pool of 209.165.200.225–209.165.200.230 serves up to 6 simultaneous sessions.

**PAT (NAT Overload):** Many-to-one mapping where multiple private IPs share a single public IP. Uses port numbers to distinguish between sessions. Use in most networks where you have many internal hosts but limited public IPs. Example: 10 hosts all share 209.165.200.226 using different source port numbers.

---

**Q53.** Compare IDS and IPS. Explain how each works, where each is placed, and the advantages and disadvantages of each.

**Model Answer:**

**IDS (Intrusion Detection System):**
- Works in **promiscuous mode** — monitors a **copy** of traffic (not inline)
- Placed **after the firewall**, not inline
- **Advantages:** No impact on network latency/jitter, no network impact if sensor fails
- **Disadvantages:** Cannot stop trigger packets (attacks get through), response actions cannot prevent the initial attack, more vulnerable to evasion techniques

**IPS (Intrusion Prevention System):**
- Works in **inline mode** — all traffic must pass through it
- Placed **after the firewall**, inline with traffic
- **Advantages:** Can stop attacks before they reach targets, can use stream normalization
- **Disadvantages:** Some impact on network latency/jitter, sensor failure or overload impacts the network

Both use signatures to detect threats, but only IPS can actively block them.

---

**Q54.** List and explain the 5 steps of IPsec VPN configuration.

**Model Answer:**

1. **Interesting Traffic** — Define which traffic should be protected using an ACL. Only traffic matching the ACL triggers the IPsec tunnel.

2. **IKE Phase 1** — Authenticate IPsec peers using pre-shared keys or RSA. Negotiate IKE SA policy (encryption, hash, DH group, authentication method, lifetime). Establish a secure channel.

3. **IKE Phase 2** — Negotiate IPsec SA parameters (transform set — which encryption/auth algorithms to use for data). Create matching IPsec SAs on both peers.

4. **Data Transfer** — Actual data is encrypted and transmitted through the IPsec tunnel using the negotiated parameters stored in the SA database.

5. **Tunnel Termination** — SAs are deleted or time out. The tunnel is torn down. New interesting traffic would restart the process.

---

**Q55.** What are the four types of IPS signature triggers? Describe each with an example.

**Model Answer:**

1. **Pattern-based (Signature-based):** Searches for specific pre-defined patterns in traffic. Example: Looking for the string "confidential" in packet payloads. Easy to configure, fewer false positives, but cannot detect unknown attacks.

2. **Policy-based (Behavior-based):** Defines suspicious behaviors based on historical analysis instead of specific patterns. Example: Flagging any SSH connection attempt from outside business hours. Can detect unknown attacks but needs custom policies.

3. **Anomaly-based (Profile-based):** Creates a baseline of "normal" network activity and flags deviations. Example: Alerting when a server suddenly receives 10x its normal traffic. Can detect unknown attacks but hard to profile large networks.

4. **Reputation-based:** Tracks reputation scores of Internet domains/IPs. Example: Blocking traffic from an IP that has sent 10M emails in 24 hours from a domain less than 24 hours old. Dynamic and effective but reputation data constantly changes.

---

**Q56.** Explain OSPF MD5 authentication: what it does, how to configure it, and what can go wrong.

**Model Answer:**

**What it does:** MD5 authentication provides secure authentication for OSPF routing updates. The password is hashed using MD5 and sent with a key ID and sequence number. The receiver computes its own hash and compares — if they match, authentication succeeds. This prevents rogue routers from injecting false routing information.

**Configuration (both routers must match):**
```
Router(config-if)# ip ospf authentication message-digest
Router(config-if)# ip ospf message-digest-key 1 md5 Cisco123
Router(config-router)# area 0 authentication message-digest
```

**What can go wrong:**
- Authentication type mismatch (one router has simple, other has MD5)
- Password mismatch (different keys configured)
- Key ID mismatch (e.g., R1 uses key 1, R2 uses key 2 — even with same password, it fails)
- Missing authentication on one side (one router has it, other doesn't)

**Important:** OSPF authentication only authenticates routing updates — it does NOT encrypt actual data traffic.

---

*End of Practice Test — Total: 56 questions*
*Time yourself: You should aim to complete this in 60–75 minutes.*