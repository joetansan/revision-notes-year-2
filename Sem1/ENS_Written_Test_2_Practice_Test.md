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

<details><summary>Click to reveal answer</summary>

**Answer: D) 110**

</details>

---

**Q2.** Which of the following OSPF packet types is used to discover neighbours and establish adjacencies?
- A) LSAck
- B) Hello
- C) LSU
- D) DBD

<details><summary>Click to reveal answer</summary>

**Answer: B) Hello**

</details>

---

**Q3.** Which IPsec protocol provides BOTH authentication and encryption?
- A) IKE
- B) AH
- C) GRE
- D) ESP

<details><summary>Click to reveal answer</summary>

**Answer: D) ESP**

</details>

---

**Q4.** What is the wildcard mask for the network 172.16.0.0/16?
- A) 0.0.255.255
- B) 0.0.0.255
- C) 255.255.0.0
- D) 255.255.255.0

<details><summary>Click to reveal answer</summary>

**Answer: A) 0.0.255.255**

</details>

---

**Q5.** Which type of firewall maintains a state table to track active connections?
- A) Application firewall
- B) Packet filtering firewall
- C) Web application firewall
- D) Stateful packet inspection firewall

<details><summary>Click to reveal answer</summary>

**Answer: D) Stateful packet inspection firewall**

</details>

---

**Q6.** Which of the following is a disadvantage of NAT?
- A) It hides internal IP addresses
- B) It conserves public IPv4 addresses
- C) It increases forwarding delays
- D) It provides address multiplexing

<details><summary>Click to reveal answer</summary>

**Answer: C) It increases forwarding delays**

</details>

---

**Q7.** Which Bluetooth attack involves accessing unauthorized information and stealing data stored on a device?
- A) Blueborne
- B) Bluebugging
- C) Bluesnarfing
- D) Bluejacking

<details><summary>Click to reveal answer</summary>

**Answer: C) Bluesnarfing**

</details>

---

**Q8.** Which IPS alarm type is the MOST dangerous?
- A) False Negative
- B) True Positive
- C) True Negative
- D) False Positive

<details><summary>Click to reveal answer</summary>

**Answer: A) False Negative**

</details>

---

**Q9.** Which command enables OSPF MD5 authentication on an interface?
- A) `area 0 authentication`
- B) `ip ospf authentication message-digest`
- C) `ip ospf authentication`
- D) `service password-encryption`

<details><summary>Click to reveal answer</summary>

**Answer: B) `ip ospf authentication message-digest`**

</details>

---

**Q10.** In which IKE phase are IPsec SA parameters negotiated?
- A) Both phases simultaneously
- B) IKE Phase 1
- C) IKE Phase 2
- D) IKE Phase 3

<details><summary>Click to reveal answer</summary>

**Answer: C) IKE Phase 2**

</details>

---

**Q11.** Which of the following is the correct number range for extended IP ACLs?
- A) 100–199
- B) 1–99
- C) 1000–1099
- D) 200–299

<details><summary>Click to reveal answer</summary>

**Answer: A) 100–199**

</details>

---

**Q12.** What does the `established` keyword in an extended ACL check for?
- A) The ACK flag is set
- B) The SYN flag is set
- C) The RST flag is set
- D) The FIN flag is set

<details><summary>Click to reveal answer</summary>

**Answer: A) The ACK flag is set**

</details>

---

**Q13.** Which NAT type maps multiple private IP addresses to a single public IP using port numbers?
- A) Dynamic NAT
- B) PAT (NAT Overload)
- C) Proxy NAT
- D) Static NAT

<details><summary>Click to reveal answer</summary>

**Answer: B) PAT (NAT Overload)**

</details>

---

**Q14.** Which wireless security protocol uses AES encryption and is the strongest?
- A) WPA2
- B) WEP
- C) WPA3
- D) WPA

<details><summary>Click to reveal answer</summary>

**Answer: A) WPA2**

</details>

---

**Q15.** What is the purpose of the Diffie-Hellman exchange in IPsec?
- A) To define interesting traffic
- B) To authenticate users
- C) To securely exchange cryptographic keys
- D) To encrypt data traffic

<details><summary>Click to reveal answer</summary>

**Answer: C) To securely exchange cryptographic keys**

</details>

---

**Q16.** Which of the following describes an IDS?
- A) A device that only filters packets based on headers
- B) An active device that blocks malicious traffic inline
- C) A device that performs NAT translations
- D) A passive device that monitors copies of traffic and generates alerts

<details><summary>Click to reveal answer</summary>

**Answer: D) A passive device that monitors copies of traffic and generates alerts**

</details>

---

**Q17.** Which OSPF authentication type sends the password in plaintext?
- A) MD5 authentication
- B) SHA authentication
- C) Simple password authentication
- D) Null authentication

<details><summary>Click to reveal answer</summary>

**Answer: C) Simple password authentication**

</details>

---

**Q18.** Which of the following is NOT a zone in a typical firewall architecture?
- A) Quarantine zone
- B) Semi-trusted zone (DMZ)
- C) Trusted zone
- D) Untrusted zone

<details><summary>Click to reveal answer</summary>

**Answer: A) Quarantine zone**

</details>

---

**Q19.** What does the `retired true` command do in IPS signature configuration?
- A) Disables the IPS entirely
- B) Stops the signature from being compiled into memory
- C) Deletes the signature permanently
- D) Removes the signature from the signature file

<details><summary>Click to reveal answer</summary>

**Answer: B) Stops the signature from being compiled into memory**

</details>

---

**Q20.** Which protocol number does ESP use?
- A) 51
- B) 47
- C) 500
- D) 50

<details><summary>Click to reveal answer</summary>

**Answer: D) 50**

</details>

---

# SECTION B: True or False

**Instructions:** Write TRUE or FALSE for each statement.

**Q21.** OSPF is a classful routing protocol.

<details><summary>Click to reveal answer</summary>

**Answer: FALSE** — OSPF is classless (sends subnet mask info).

</details>

---

**Q22.** Standard ACLs should be placed closest to the source of traffic.

<details><summary>Click to reveal answer</summary>

**Answer: FALSE** — Standard ACLs should be placed closest to the destination.

</details>

---

**Q23.** The implicit "deny any" at the end of every ACL is visible in the configuration.

<details><summary>Click to reveal answer</summary>

**Answer: FALSE** — It is invisible/implicit but always present.

</details>

---

**Q24.** ESP operates on IP protocol number 50.

<details><summary>Click to reveal answer</summary>

**Answer: TRUE**

</details>

---

**Q25.** PAT uses source port numbers to distinguish between sessions from different internal hosts.

<details><summary>Click to reveal answer</summary>

**Answer: TRUE**

</details>

---

**Q26.** An IPS sensor in promiscuous mode can stop attacks before they reach the target.

<details><summary>Click to reveal answer</summary>

**Answer: FALSE** — Promiscuous mode is IDS (passive, alerts only). IPS inline mode can stop attacks.

</details>

---

**Q27.** WEP uses the RC4 encryption algorithm.

<details><summary>Click to reveal answer</summary>

**Answer: TRUE**

</details>

---

**Q28.** OSPF MD5 authentication encrypts the actual data traffic between routers.

<details><summary>Click to reveal answer</summary>

**Answer: FALSE** — OSPF authentication only authenticates routing updates, it does NOT encrypt data traffic.

</details>

---

**Q29.** A composite IPS signature requires state information and can span multiple packets.

<details><summary>Click to reveal answer</summary>

**Answer: TRUE**

</details>

---

**Q30.** The `service password-encryption` command encrypts OSPF routing updates.

<details><summary>Click to reveal answer</summary>

**Answer: FALSE** — It only encrypts passwords displayed in the running configuration file.

</details>

---

# SECTION C: Multi-Select Questions

**Instructions:** Choose ALL correct answers.

**Q31.** Which three parameters must match for two OSPF routers to become neighbours? (Choose three.)
- A) Hello interval
- B) Process ID
- C) Dead interval
- D) Network type
- E) Router ID

<details><summary>Click to reveal answer</summary>

**Answer: A, C, D** — Hello interval, Dead interval, and Network type must match. Process ID is locally significant only, and Router IDs must be unique (not matching).

</details>

---

**Q32.** Which two services does ESP provide? (Choose two.)
- A) Confidentiality (encryption)
- B) Routing
- C) Authentication and integrity
- D) NAT translation
- E) DHCP

<details><summary>Click to reveal answer</summary>

**Answer: A, C** — ESP provides confidentiality (encryption) plus authentication and integrity.

</details>

---

**Q33.** Which two are characteristics of NGFWs? (Choose two.)
- A) Application awareness
- B) Only works at Layer 3
- C) Identity awareness
- D) Cannot inspect encrypted traffic
- E) No integration with IPS

<details><summary>Click to reveal answer</summary>

**Answer: A, C** — NGFWs have application awareness (L2–L7) and identity awareness (integrates with AD/LDAP).

</details>

---

**Q34.** Which two commands are required to enable IPS SDEE message logging? (Choose two.)
- A) `logging on`
- B) `ip ips notify log`
- C) `ip http server`
- D) `ip ips notify sdee`
- E) `ip sdee events 500`

<details><summary>Click to reveal answer</summary>

**Answer: C, D** — `ip http server` must be enabled first (SDEE works over HTTP), then `ip ips notify sdee` enables SDEE notification.

</details>

---

**Q35.** Which are private IP address ranges according to RFC 1918? (Choose three.)
- A) 10.0.0.0 – 10.255.255.255
- B) 11.0.0.0 – 11.255.255.255
- C) 172.16.0.0 – 172.31.255.255
- D) 192.168.0.0 – 192.168.255.255
- E) 169.254.0.0 – 169.254.255.255

<details><summary>Click to reveal answer</summary>

**Answer: A, C, D** — Class A: 10.0.0.0/8, Class B: 172.16.0.0/12, Class C: 192.168.0.0/16. (169.254.x.x is APIPA/link-local, not RFC 1918 private.)

</details>

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

<details><summary>Click to reveal answer</summary>

**Answer: 1-C, 2-D, 3-B, 4-E, 5-A**

</details>

---

**Q37.** Match each IPS alarm type to its description.

| # | Alarm Type | | Description |
|---|------------|---|-------------|
| 1 | True Positive | ___ | A) Alarm generated for normal user traffic |
| 2 | False Positive | ___ | B) No alarm generated for attack traffic |
| 3 | True Negative | ___ | C) Alarm generated for attack traffic |
| 4 | False Negative | ___ | D) No alarm generated for normal user traffic |

<details><summary>Click to reveal answer</summary>

**Answer: 1-C, 2-A, 3-D, 4-B**

</details>

---

**Q38.** Match each wireless attack to its description.

| # | Attack | | Description |
|---|--------|---|-------------|
| 1 | Evil Twin | ___ | A) Sending unsolicited messages to Bluetooth devices |
| 2 | Rogue AP | ___ | B) Mimics a legitimate AP so users connect to it |
| 3 | Bluejacking | ___ | C) Unauthorized AP installed on a secure network |
| 4 | Bluesnarfing | ___ | D) Stealing data from a Bluetooth device |

<details><summary>Click to reveal answer</summary>

**Answer: 1-B, 2-C, 3-A, 4-D**

</details>

---

**Q39.** Match each firewall type to the OSI layer(s) it operates on.

| # | Firewall Type | | OSI Layer(s) |
|---|---------------|---|-------------|
| 1 | Packet Filtering | ___ | A) Layers 3, 4, 5, 7 |
| 2 | Stateful Inspection | ___ | B) Layer 3 (sometimes 4) |
| 3 | Application Firewall | ___ | C) Layers 3–4 |

<details><summary>Click to reveal answer</summary>

**Answer: 1-B, 2-C, 3-A**

</details>

---

**Q40.** Match each NAT term to its description.

| # | Term | | Description |
|---|------|---|-------------|
| 1 | Inside Local | ___ | A) Address of source as seen from outside network |
| 2 | Inside Global | ___ | B) Address of destination as seen from outside |
| 3 | Outside Global | ___ | C) Address of source as seen from inside (private) |
| 4 | Outside Local | ___ | D) Address of destination as seen from inside |

<details><summary>Click to reveal answer</summary>

**Answer: 1-C, 2-A, 3-B, 4-D**

</details>

---

# SECTION E: Fill in the Blanks

**Q41.** OSPF uses a default Administrative Distance of _______.

<details><summary>Click to reveal answer</summary>

**Answer: 110**

</details>

---

**Q42.** The three parameters that must match for OSPF neighbours are: _______, _______, and _______.

<details><summary>Click to reveal answer</summary>

**Answer: Hello interval, Dead interval, Network type**

</details>

---

**Q43.** An ACL is a sequential series of _______ that tell the router what packets to accept or _______.

<details><summary>Click to reveal answer</summary>

**Answer: filters/statements, deny/drop**

</details>

---

**Q44.** The IPsec protocol that provides authentication and integrity but NOT encryption is called _______.

<details><summary>Click to reveal answer</summary>

**Answer: AH (Authentication Header)**

</details>

---

**Q45.** The process of translating multiple private IP addresses to a single public IP using port numbers is called _______ or _______.

<details><summary>Click to reveal answer</summary>

**Answer: PAT (Port Address Translation), NAT Overload**

</details>

---

**Q46.** WEP's Initialization Vector (IV) is only _______ bits long, which creates approximately _______ possible values.

<details><summary>Click to reveal answer</summary>

**Answer: 24, 16 million (2^24)**

</details>

---

**Q47.** An IPS signature that consists of a single packet and requires no state information is called an _______ signature.

<details><summary>Click to reveal answer</summary>

**Answer: Atomic**

</details>

---

**Q48.** The command _______ is used to apply a standard ACL to an interface, while _______ is used to restrict VTY access.

<details><summary>Click to reveal answer</summary>

**Answer: ip access-group, access-class**

</details>

---

**Q49.** In IKE, Phase 1 authenticates peers and establishes a secure channel, while Phase 2 negotiates _______ parameters.

<details><summary>Click to reveal answer</summary>

**Answer: IPsec SA (Security Association)**

</details>

---

**Q50.** A _______ positive alarm occurs when the IPS generates an alarm for normal user traffic that should not have triggered an alarm.

<details><summary>Click to reveal answer</summary>

**Answer: False**

</details>

---

# SECTION F: Open-Ended Questions

**Q51.** Explain the difference between Standard ACLs and Extended ACLs. Include number ranges, what they can filter on, and recommended placement.

<details><summary>Click to reveal model answer</summary>

**Model Answer:**
Standard ACLs (numbered 1–99) can only filter on the **source IP address**. They should be placed **closest to the destination** because they can't distinguish between different destinations — placing them near the source would block all traffic from that host.

Extended ACLs (numbered 100–199) can filter on **source IP, destination IP, protocol (TCP/UDP/ICMP), and port numbers**. They should be placed **closest to the source** because they can precisely match on destination, and filtering early saves bandwidth by dropping unwanted traffic before it traverses the network.

Both types have an implicit "deny any" at the end and must be applied to an interface using `ip access-group`.

</details>

---

**Q52.** Describe the three types of NAT (Static, Dynamic, PAT). For each, explain how it works, when you would use it, and give an example.

<details><summary>Click to reveal model answer</summary>

**Model Answer:**

**Static NAT:** One-to-one permanent mapping between a private IP and a public IP. The mapping never changes. Use for devices that need a consistent public address accessible from the Internet, such as web servers. Example: 192.168.1.10 is always mapped to 209.165.200.225.

**Dynamic NAT:** Many-to-many mapping from a pool of public IPs. When an inside device needs Internet access, it grabs an available public IP from the pool on a first-come, first-served basis. Use when you have more public IPs than simultaneous users. Example: A pool of 209.165.200.225–209.165.200.230 serves up to 6 simultaneous sessions.

**PAT (NAT Overload):** Many-to-one mapping where multiple private IPs share a single public IP. Uses port numbers to distinguish between sessions. Use in most networks where you have many internal hosts but limited public IPs. Example: 10 hosts all share 209.165.200.226 using different source port numbers.

</details>

---

**Q53.** Compare IDS and IPS. Explain how each works, where each is placed, and the advantages and disadvantages of each.

<details><summary>Click to reveal model answer</summary>

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

</details>

---

**Q54.** List and explain the 5 steps of IPsec VPN configuration.

<details><summary>Click to reveal model answer</summary>

**Model Answer:**

1. **Interesting Traffic** — Define which traffic should be protected using an ACL. Only traffic matching the ACL triggers the IPsec tunnel.

2. **IKE Phase 1** — Authenticate IPsec peers using pre-shared keys or RSA. Negotiate IKE SA policy (encryption, hash, DH group, authentication method, lifetime). Establish a secure channel.

3. **IKE Phase 2** — Negotiate IPsec SA parameters (transform set — which encryption/auth algorithms to use for data). Create matching IPsec SAs on both peers.

4. **Data Transfer** — Actual data is encrypted and transmitted through the IPsec tunnel using the negotiated parameters stored in the SA database.

5. **Tunnel Termination** — SAs are deleted or time out. The tunnel is torn down. New interesting traffic would restart the process.

</details>

---

**Q55.** What are the four types of IPS signature triggers? Describe each with an example.

<details><summary>Click to reveal model answer</summary>

**Model Answer:**

1. **Pattern-based (Signature-based):** Searches for specific pre-defined patterns in traffic. Example: Looking for the string "confidential" in packet payloads. Easy to configure, fewer false positives, but cannot detect unknown attacks.

2. **Policy-based (Behavior-based):** Defines suspicious behaviors based on historical analysis instead of specific patterns. Example: Flagging any SSH connection attempt from outside business hours. Can detect unknown attacks but needs custom policies.

3. **Anomaly-based (Profile-based):** Creates a baseline of "normal" network activity and flags deviations. Example: Alerting when a server suddenly receives 10x its normal traffic. Can detect unknown attacks but hard to profile large networks.

4. **Reputation-based:** Tracks reputation scores of Internet domains/IPs. Example: Blocking traffic from an IP that has sent 10M emails in 24 hours from a domain less than 24 hours old. Dynamic and effective but reputation data constantly changes.

</details>

---

**Q56.** Explain OSPF MD5 authentication: what it does, how to configure it, and what can go wrong.

<details><summary>Click to reveal model answer</summary>

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

</details>

---

*End of Practice Test — Total: 56 questions*
*Time yourself: You should aim to complete this in 60–75 minutes.*
