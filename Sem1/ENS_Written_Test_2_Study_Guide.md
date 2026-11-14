# Enterprise Network Security — Written Test 2 Study Guide
## Topics: Week 5, 6, 7, 8, 11, 12, 13
## Test Format: MCQ, True/False, Multi-Select, Match-the-Following, Fill-in-the-Blanks, Open-Ended
## Duration: 1 hour 15 minutes | Weightage: 30%

---

# UNIT 1: OSPF Routing and Security (Week 5)

## 1.1 What is OSPF?

**Core Concept:** OSPF (Open Shortest Path First) is a **classless, link-state routing protocol**. It is an open standard (works across different vendors), and is known for scalability.

- **Classless** → It sends subnet mask information with route updates (supports VLSM/CIDR).
- **Link-state** → Each router independently calculates the best path to every destination using a complete map (topology) of the network.
- **Open standard** → Defined by IETF (not proprietary like EIGRP).

**Why it matters:** OSPF is the most widely used Interior Gateway Protocol (IGP) in enterprise networks. It converges fast and scales well.

**How the professor expects it:** Know the definition, know that it's classless and link-state. Expect MCQ/True-False asking "OSPF is a classless routing protocol" → TRUE.

---

## 1.2 OSPF Packet Types (LSPs)

There are **5 types** of OSPF packets (Link-State Packets):

| Packet | Full Name | Purpose |
|--------|-----------|---------|
| **Hello** | Hello | Discover neighbors, establish & maintain adjacency |
| **DBD** | Database Description | Abbreviated list of the sending router's link-state database |
| **LSR** | Link-State Request | Request more info about an entry in the DBD |
| **LSU** | Link-State Update | Carries link-state information (actual LSAs) |
| **LSAck** | LSA Acknowledgment | Confirms receipt of the LSU |

**Memory tip:** "Hello, Database Describes, Requests Updates, and gets Acknowledged"

**How the professor expects it:** Match-the-following questions pairing packet names with descriptions. Know all 5 by name and function.

---

## 1.3 Hello Packets & Neighbour Establishment

**Core Concept:** Hello packets are sent periodically to discover OSPF neighbours and maintain adjacencies.

For two routers to become neighbours, **3 parameters must match**:
1. **Hello interval** — how often Hello packets are sent
2. **Dead interval** — how long to wait before declaring a neighbour dead
3. **Network type** — must agree (e.g., both Ethernet)

**Default values on Ethernet:**
- Hello interval: **10 seconds**
- Dead interval: **40 seconds**

**Process:**
1. Routers exchange Hello packets
2. If the 3 parameters match → they become **neighbours**
3. They exchange DBDs (Database Descriptions)
4. They exchange LSUs and LSAs
5. **Full adjacency** is reached when both routers have identical link-state databases

**How the professor expects it:** "What causes OSPF adjacency to fail?" → Different dead timers, different Hello intervals, different network types. Also: "What are the 3 parameters that must match?"

---

## 1.4 Router ID

**Core Concept:** A **Router ID** uniquely identifies each OSPF router. It's a 32-bit number (looks like an IP address).

**Configuration:**
```
R1(config)# router ospf 10
R1(config-router)# router-id 1.1.1.1
```

**Key point:** The process-id (e.g., 10) is **locally significant only** — it does NOT have to match on different routers.

---

## 1.5 OSPF Network Statement

**Core Concept:** You must tell OSPF which networks to advertise using the `network` command:

```
R1(config-router)# network 172.16.3.0 0.0.0.3 area 0
```

- The second parameter is the **wildcard mask** (inverse of subnet mask)
- `area 0` is the **backbone area** — all areas must connect to Area 0
- If you don't advertise a network, other routers won't know about it

**How the professor expects it:** Configuration questions — "Write the OSPF network command to advertise 192.168.1.0/24 in Area 0."

---

## 1.6 Passive Interface

**Core Concept:** A passive interface **does not send OSPF Hello packets/LSAs** out. This is useful for interfaces connected to switches/PCs (not to other routers) — saves bandwidth.

```
R1(config-router)# passive-interface g0/0
```

**Why it matters:** Without passive-interface, OSPF wastes bandwidth sending Hellos to devices that don't understand OSPF.

---

## 1.7 Administrative Distance (AD)

**Core Concept:** AD is the **trustworthiness** of a route source. Lower AD = more trusted.

| Route Source | Default AD |
|-------------|-----------|
| Directly connected | 0 |
| Static route | 1 |
| **OSPF** | **110** |
| EIGRP | 90 |
| RIP | 120 |

**Example:** If both a static route and OSPF can reach 10.1.1.1, the router picks the static route (AD=1) over OSPF (AD=110).

**How the professor expects it:** MCQ: "What is the default AD of OSPF?" → 110.

---

## 1.8 Verifying OSPF Operation

| Command | What it shows |
|---------|---------------|
| `show ip ospf neighbors` | Adjacent OSPF routers (neighbours) |
| `show ip route` | Routing table (remote routes learned via OSPF marked with "O") |
| `show ip protocols` | Process ID, Router ID, networks advertised, neighbour routers |

---

## 1.9 OSPF Authentication

**Core Concept:** OSPF supports authentication to prevent rogue routers from injecting false routing updates.

**Three types:**

| Type | Number | Security | Description |
|------|--------|----------|-------------|
| **Null** | Type 0 | None | Default — no authentication |
| **Simple Password** | Type 1 | Weak | Password sent in **plaintext** (can be sniffed) |
| **MD5** | Type 2 | Strong | Password is hashed using MD5 (never sent in clear) |

### Simple Password Authentication
```
R1(config-if)# ip ospf authentication
R1(config-if)# ip ospf authentication-key Cisco123
R1(config-router)# area 0 authentication
```
- Passwords must match between **neighbours** (not necessarily across the whole area)
- Vulnerable to sniffing — password is sent in plaintext

### MD5 Authentication
```
R1(config-if)# ip ospf authentication message-digest
R1(config-if)# ip ospf message-digest-key 1 md5 Cisco123
R1(config-router)# area 0 authentication message-digest
```
- Uses a **key ID** and a **key** — both must match on neighbours
- The password is hashed, not sent in the clear

**Key difference:** Simple = plaintext, MD5 = hashed. MD5 is more secure.

**Troubleshooting:** If OSPF adjacency fails after enabling authentication:
- Check that both routers use the same authentication type
- Check that passwords match
- Check that key IDs match (for MD5)

### Service Password Encryption
```
R1(config)# service password-encryption
```
- Encrypts passwords in the running configuration file (so they can't be read in plaintext from `show run`)
- Does NOT encrypt the actual OSPF traffic

**How the professor expects it:** 
- "What does OSPF authentication protect against?" → Prevents exchanging routing info with rogue routers, prevents packet sniffing of OSPF info. It does NOT protect actual data traffic.
- Configuration questions: Write the commands for MD5 authentication.
- Troubleshooting: "R1 and R2 can't form OSPF adjacency. R1 has MD5 key 1, R2 has MD5 key 2 with the same password. What's wrong?" → Key IDs must match.

---

## 1.10 Default Route Propagation in OSPF

**Core Concept:** You can propagate a default route through OSPF so other routers know where to send traffic for unknown destinations.

```
R1(config)# ip route 0.0.0.0 0.0.0.0 serial0/0/0
R1(config-router)# default-information originate
```

**Warning:** Without proper configuration, this can cause routing loops.

---

# UNIT 2: Access Control Lists (Week 6)

## 2.1 What are ACLs?

**Core Concept:** An ACL (Access Control List) is a **sequential series of filters** that tell a router what packets to **accept (permit)** or **deny (drop)** based on specified conditions.

**Key rules:**
1. ACLs are evaluated **top-down** — first match wins, rest is skipped
2. There is an **implicit "deny any"** at the end of every ACL (invisible, always there)
3. **One ACL per protocol, per interface, per direction** (e.g., one inbound IP ACL on Fa0/0)
4. ACLs do NOT block traffic that **originates from the router itself**
5. You must **apply** the ACL to an interface for it to take effect

**Why it matters:** ACLs are the primary method of traffic filtering on routers — used for security, traffic control, and defining "interesting traffic" for VPNs.

---

## 2.2 Standard vs Extended ACLs

| Feature | Standard ACL | Extended ACL |
|---------|-------------|--------------|
| **Number range** | 1–99 (and 1300–1999) | 100–199 (and 2000–2699) |
| **Filters on** | **Source IP only** | Source IP, Destination IP, Protocol, Port numbers |
| **Placement** | **Closest to destination** | **Closest to source** |
| **Flexibility** | Limited | Very flexible |

**Why standard ACLs go near destination:** They filter on source only — if placed near source, they'd block ALL traffic from that host, even legitimate traffic to other destinations.

**Why extended ACLs go near source:** They can filter on destination too, so placing them near source saves bandwidth by dropping unwanted traffic early.

---

## 2.3 Standard ACL Configuration (2 Steps)

**Step 1: Define the ACL**
```
RouterB(config)# access-list 10 permit host 172.16.30.2
RouterB(config)# access-list 10 deny 0.0.0.0 255.255.255.255
```
- `permit` or `deny` + source address + wildcard mask
- The implicit deny any is already there — the explicit deny is optional but makes it visible

**Step 2: Apply to an interface**
```
RouterB(config)# interface e0
RouterB(config-if)# ip access-group 10 in
```

**The `host` keyword:**
- `access-list 10 permit 192.168.1.100 0.0.0.0` = same as `access-list 10 permit host 192.168.1.100`

---

## 2.4 Wildcard Masks

**Core Concept:** A wildcard mask tells the router **how much of the address must match**. It is the **inverse of a subnet mask**.

| Subnet Mask | Wildcard Mask |
|-------------|--------------|
| 255.255.255.0 (/24) | 0.0.0.255 |
| 255.255.0.0 (/16) | 0.0.255.255 |
| 255.255.255.252 (/30) | 0.0.0.3 |

**How to calculate:** Wildcard = 255.255.255.255 − Subnet Mask

**Common mistake:** ACLs use **wildcard masks**, NOT subnet masks. `access-list 10 permit 185.64.0.0 255.255.0.0` is WRONG — it should be `0.0.255.255`.

**Special wildcard:**
- `0.0.0.0` = match exactly this one address (use `host` keyword instead)
- `255.255.255.255` = match any address (use `any` keyword instead)

**How the professor expects it:** MCQ asking which wildcard mask is correct for a given network. Also: "Which command will allow only traffic from network 185.64.0.0 to enter interface s0?" — need to know the correct wildcard.

---

## 2.5 Extended ACL Configuration

**Core Concept:** Extended ACLs can filter on source IP, destination IP, protocol (TCP/UDP/ICMP), and port numbers.

```
RouterA(config)# access-list 110 permit tcp host 172.16.50.2 host 172.16.10.2 eq 80
RouterA(config)# interface e0
RouterA(config-if)# ip access-group 110 out
```

**Syntax:** `access-list <100-199> permit|deny <protocol> <source> <source-wildcard> <destination> <destination-wildcard> [operator <port>]`

**Operators:** `eq` (equal), `gt` (greater than), `lt` (less than), `ne` (not equal)

**Common ports to know:**
- HTTP = 80
- HTTPS = 443
- Telnet = 23
- SSH = 22
- FTP = 20 (data), 21 (control)
- DNS = 53
- SMTP = 25

---

## 2.6 Named ACLs

**Core Concept:** Named ACLs use alphanumeric names instead of numbers. Advantages:
1. Easier to identify (e.g., "BLOCK-TELNET" instead of "101")
2. No limit on number of ACLs
3. Can delete individual statements (but can only add to the end)

**Standard Named ACL:**
```
Router(config)# ip access-list standard BLOCK-SALES
Router(config-std-nacl)# permit host 192.168.1.100
Router(config-std-nacl)# deny any
Router(config)# interface fa0/0
Router(config-if)# ip access-group BLOCK-SALES in
```

**Extended Named ACL:**
```
Router(config)# ip access-list extended NO-HTTP
Router(config-ext-nacl)# deny tcp 192.168.1.0 0.0.0.255 any eq 80
Router(config-ext-nacl)# permit ip any any
```

---

## 2.7 Restricting VTY (Telnet/SSH) Access

**Core Concept:** You can use ACLs to control who can remotely access (Telnet/SSH) the router itself.

```
Rt1(config)# access-list 2 permit host 192.168.1.100
Rt1(config)# line vty 0 5
Rt1(config-line)# login
Rt1(config-line)# password secret
Rt1(config-line)# access-class 2 in
```
- Note: Uses `access-class`, NOT `access-group`

---

## 2.8 Advanced ACLs

### TCP Established ACL
**Core Concept:** The `established` keyword allows only return traffic for TCP connections initiated from inside the network.

```
R1(config)# access-list 100 permit tcp any eq 443 192.168.1.0 0.0.0.255 established
R1(config)# access-list 100 deny ip any any
R1(config)# interface s0/0/0
R1(config-if)# ip access-group 100 in
```

- Checks if the TCP **ACK flag** is set → if yes, it's return traffic → permit
- If ACK is NOT set → it's a new connection from outside → deny
- **Important:** This does NOT implement a stateful firewall — no state table is maintained

### Time-Based ACLs
**Core Concept:** ACLs that only apply during specific times.

```
R1(config)# time-range EMPLOYEE-TIME
R1(config-time-range)# periodic weekdays 12:00 to 13:00
R1(config-time-range)# periodic weekdays 17:00 to 19:00
R1(config)# access-list 100 permit ip 192.168.1.0 0.0.0.255 any time-range EMPLOYEE-TIME
R1(config)# access-list 100 deny ip any any
```

---

# UNIT 3: Firewalls (Week 7)

## 3.1 What is a Firewall?

**Core Concept:** A firewall is a system that **controls access between two networks** — a trusted network (internal) and an untrusted network (Internet). It intercepts and controls traffic based on security policies.

**Purpose:**
- Perimeter defence
- Log inter-network activity
- Limit exposure of the organization

**Challenges:** Firewalls cannot fully handle: malware from inside, connections that bypass the firewall, unknown threats, poorly trained administrators.

---

## 3.2 Three Types of Firewalls

### 1. Packet Filtering Firewall
- Operates at **Layer 3 (Network)** and sometimes Layer 4
- Makes decisions based on **packet header** (source/dest IP, port numbers)
- **Stateless** — each packet examined independently, no memory of previous packets
- Fast but limited security

### 2. Stateful Packet Inspection (SPI) / Stateful Firewall
- Operates at **Layer 3–4**
- Maintains a **state table** tracking active connections
- Knows if a packet belongs to an existing, valid session
- Tracks TCP sequence numbers
- Can detect and drop packets with no valid connection
- **Drawback:** Cannot prevent Trojans/spyware where the connection was initiated from INSIDE the network

### 3. Application Firewall (Proxy Firewall)
- Operates at **Layers 3, 4, 5, and 7**
- Examines the **application layer data** (content inspection)
- Can inspect HTTP, FTP, etc. at the application level
- Also called **Deep Packet Inspection (DPI)** when it examines the data part of packets

**Key comparison:**

| Feature | Packet Filter | Stateful SPI | Application Firewall |
|---------|--------------|-------------|---------------------|
| OSI Layer | 3 | 3–4 | 3, 4, 5, 7 |
| State tracking | No | Yes | Yes |
| Content inspection | No | No | Yes |
| Speed | Fastest | Fast | Slower |

**How the professor expects it:** "Which firewall does NOT act on the Application layer?" → Packet Filtering. Match-the-following: firewall type vs OSI layer.

---

## 3.3 Next Generation Firewall (NGFW)

**Core Concept:** NGFW goes beyond traditional firewalls with:

1. **Application Awareness** — Doesn't assume apps run on standard ports. Monitors L2–L7 with granularity.
2. **Identity Awareness** — Tracks which user/device is generating traffic (integrates with Active Directory/LDAP)
3. **Extra Intelligence** — Uses whitelists, blacklists, directory integration
4. **Integrated IPS** — Automatically correlates with IPS to suggest blocking malicious traffic

**Why NGFW was needed:**
- Botnets invisible to first-gen firewalls
- HTTP/HTTPS used for everything → port-based rules less useful
- Traditional firewalls can't identify application misuse

---

## 3.4 Web Application Firewall (WAF)

- Example: **ModSecurity** (open source)
- Acts as an inbound proxy to web servers (Apache, IIS)
- Inspects HTTP/HTTPS request and response data
- Detects: SQL injection, XSS, cookie tampering, buffer overflow
- Uses OWASP core rule set (free)

---

## 3.5 Unified Threat Management (UTM)

**Core Concept:** An all-in-one appliance combining:
- Firewall
- IDS/IPS
- SIEM
- Secure Web/Email Gateway
- Remote Access

Popular with SMEs (Small Medium Enterprises). Browser-based management, short learning curve.

---

## 3.6 Firewall Zones

Three typical zones:
1. **Trusted Zone** — Internal private network
2. **Untrusted Zone** — Internet
3. **Semi-trusted Zone (DMZ)** — Publicly accessible servers (web servers, email servers)

```
Internet (Untrusted) ←→ Firewall ←→ DMZ (Semi-trusted)
                              ↕
                    Internal LAN (Trusted)
```

---

## 3.7 Firewall Policy Design

**Core Concept:** Filtering rules are applied **in order** — first match wins.

**Example: Filtering Telnet**

| Rule | Direction | Source | Dest | Protocol | Src Port | Dst Port | Action |
|------|-----------|--------|------|----------|----------|----------|--------|
| 1 | Out | Internal | Any | TCP | >1023 | 23 | Permit |
| 2 | In | Any | Internal | TCP | 23 | >1023 | Permit |
| 3 | Any | Any | Any | Any | Any | Any | **Deny** |

**Two strategies for ordering rules:**
1. Most specific → most general (prevent general rule from overriding specific)
2. Most frequently used rules at top (performance)

---

## 3.8 Firewall Best Practices

1. **Deny all** traffic by default; only enable needed services
2. Disable unnecessary services/software on the firewall
3. Limit applications running on the firewall
4. Run firewall as unique user (not admin/root)
5. Change default admin password
6. Don't rely on packet filtering alone — use stateful inspection and proxies
7. Control physical access to the firewall
8. Regularly monitor firewall logs
9. Document all firewall rule changes

**How the professor expects it:** List/describe best practices in open-ended questions. Know the three firewall types and their OSI layers.

---

## 3.9 Difference between Firewalls, IDS, and IPS

| Parameter | Firewall (SPI) | IPS | IDS |
|-----------|---------------|-----|-----|
| **Definition** | Filters traffic based on rules | Inspects & stops malicious traffic | Monitors & alerts on malicious traffic |
| **Detects based on** | IP addresses, port numbers | Traffic patterns & signatures | Traffic patterns & signatures |
| **Layer** | Layer 3 | Layers 2+ | Layers 2+ |
| **Placement** | 1st line of defence | After firewall, **inline** | After firewall, **not inline** |
| **Action** | Blocks traffic | **Blocks** attacks | **Alerts only** |

---

# UNIT 4: VPN and IPsec (Week 8)

## 4.1 What is a VPN?

**Core Concept:** A Virtual Private Network (VPN) creates a **private, encrypted tunnel** over a public network (usually the Internet). It provides the same security as private WAN links but at much lower cost.

**VPN Services:**
- **Authentication** — verifying identities
- **Data Integrity** — ensuring data isn't modified in transit
- **Confidentiality** — encrypting data so others can't read it

**Benefits:** Cost savings, security, scalability, compatibility with broadband.

---

## 4.2 VPN Classifications

### By Architecture:
| Type | Description | Tunnel Endpoints |
|------|-------------|-----------------|
| **Intranet VPN** | Site-to-site, connects branch offices to HQ | Fixed |
| **Extranet VPN** | Site-to-site, connects trading partners | Fixed |
| **Remote VPN** | User-to-LAN, connects mobile users | Variable |

### By Tunnelling:
- **Voluntary Tunnel** — Created by the client PC (end-to-end)
- **Compulsory Tunnel** — Created by an intermediate device (VPN gateway), shared by multiple users

### By OSI Layer:
| Layer | Protocol |
|-------|----------|
| Layer 2 | PPP |
| Layer 3 | **IPsec** |
| Layer 4/7 | SSL VPN, Cisco WebVPN |

---

## 4.3 GRE vs IPsec

| Feature | GRE | IPsec |
|---------|-----|-------|
| Encapsulates | Almost any packet type | IP only |
| Supports multicast/routing protocols | Yes | No (unicast only) |
| Encryption | No (by itself) | Yes |
| Protocol number | 47 (IP protocol) | AH=51, ESP=50 |
| Overhead | 24 bytes | Varies |

**When to use which:**
- **GRE** → When you need multiprotocol/multicast support (e.g., routing protocols over tunnel)
- **IPsec** → When you need encryption and security
- **GRE over IPsec** → Best of both worlds (GRE for multicast + IPsec for encryption)

---

## 4.4 IPsec Framework

**Core Concept:** IPsec is a **framework of open standards** (by IETF) for secure IP communications. It's NOT tied to specific algorithms — newer algorithms can be plugged in.

**IPsec provides:**
1. **Confidentiality** (encryption) — DES, 3DES, AES, SEAL
2. **Integrity** (data not tampered) — HMAC-MD5, HMAC-SHA
3. **Authentication** (identity verification) — PSK (Pre-Shared Key), RSA
4. **Secure Key Exchange** — Diffie-Hellman (DH groups 1, 2, 5, 7)

---

## 4.5 IPsec Protocols: AH vs ESP

### Authentication Header (AH)
- Protocol number: **51**
- Provides: **Authentication + Integrity** (NOT encryption)
- All text is transported **unencrypted**
- Uses HMAC-MD5 or HMAC-SHA-1
- Use when confidentiality is NOT required

### Encapsulating Security Payload (ESP)
- Protocol number: **50**
- Provides: **Authentication + Integrity + Encryption**
- Encrypts using DES, 3DES, AES, or SEAL
- Then hashes for integrity using HMAC-MD5 or HMAC-SHA-1
- **Most commonly used** in IPsec VPNs

**Key exam point:** "Which IPsec protocol provides confidentiality?" → **ESP** (AH does NOT encrypt)

---

## 4.6 Transport Mode vs Tunnel Mode

| Feature | Transport Mode | Tunnel Mode |
|---------|---------------|-------------|
| **What's protected** | Payload only (L4+) | Entire original IP packet |
| **Original IP header** | Visible (plaintext) | Hidden (encrypted) |
| **Use case** | Host-to-host communication | Site-to-site VPN, Remote access |
| **IP-in-IP** | No | Yes (new IP header added) |

**How the professor expects it:** "When using ESP tunnel mode, which part is NOT authenticated?" → The **new IP header** (outer header).

---

## 4.7 Internet Key Exchange (IKE)

**Core Concept:** IKE is the protocol that **securely negotiates** IPsec parameters between peers. It uses UDP **port 500**.

**IKE has 2 phases:**

### IKE Phase 1 — "Build the secure channel"
- Authenticates the IPsec peers
- Negotiates IKE SA (Security Association) policy
- Performs authenticated Diffie-Hellman key exchange
- Sets up a secure tunnel for Phase 2
- Two modes: **Main Mode** (6 messages) or **Aggressive Mode** (3 messages)

**Phase 1 Policy Parameters that must match:**
- Encryption algorithm (DES, 3DES, AES)
- Hash algorithm (MD5, SHA)
- Authentication method (PSK, RSA)
- Diffie-Hellman group (1, 2, 5)
- Lifetime (in seconds)

### IKE Phase 2 — "Negotiate IPsec parameters"
- Negotiates IPsec SA parameters (transform sets)
- Establishes IPsec security associations
- Periodically renegotiates IPsec SAs
- Optionally performs additional DH exchange

**Key distinction:**
- Phase 1 = protect the **IKE negotiation** itself
- Phase 2 = negotiate the **IPsec parameters** for data protection

---

## 4.8 Security Associations (SA)

**Core Concept:** An SA is a relationship between peers that describes how they'll use IPsec to protect traffic.

**An SA is identified by 3 parameters:**
1. **SPI** (Security Parameter Index) — a number identifying the SA
2. **IP Destination Address** — address of the destination device
3. **Security Protocol** — AH or ESP

**How the professor expects it:** "What are the 3 parameters that identify an SA?" → SPI, IP destination address, Security protocol (AH/ESP).

---

## 4.9 Five Steps of IPsec Transmission

1. **Interesting Traffic** — Define what traffic triggers IPsec (using ACLs)
2. **IKE Phase 1** — Authenticate peers, establish secure channel
3. **IKE Phase 2** — Negotiate IPsec SA parameters
4. **Data Transfer** — Actual encrypted data flows
5. **Tunnel Termination** — SAs are deleted or time out

---

## 4.10 Configuring IPsec VPN (Key Commands)

### Step 1: Configure ISAKMP (IKE Phase 1) policy
```
R1(config)# crypto isakmp policy 100
R1(config-isakmp)# authentication pre-share
R1(config-isakmp)# encryption 3des
R1(config-isakmp)# group 2
R1(config-isakmp)# hash sha
R1(config-isakmp)# lifetime 43200
```

### Step 2: Define pre-shared key
```
R1(config)# crypto isakmp key C1sc0 address 172.30.2.2
```

### Step 3: Configure IPsec transform set (IKE Phase 2)
```
R1(config)# crypto ipsec transform-set MY-SET esp-des esp-sha-hmac
```

### Step 4: Define interesting traffic (ACL)
```
R1(config)# access-list 102 permit ip host 172.30.1.2 host 172.30.2.2
```

### Step 5: Create crypto map and apply to interface
```
R1(config)# crypto map MYMAP 10 ipsec-isakmp
R1(config-crypto-map)# set peer 172.30.2.2
R1(config-crypto-map)# set transform-set MY-SET
R1(config-crypto-map)# match address 102
R1(config)# interface e0/1
R1(config-if)# crypto map MYMAP
```

### Verification Commands:
- `show crypto isakmp policy` — View IKE Phase 1 policies
- `show crypto ipsec transform-set` — View transform sets
- `show crypto ipsec sa` — View active IPsec SAs
- `show crypto map` — View crypto map configuration
- `clear crypto sa` — Clear IPsec SAs

---

## 4.11 ISAKMP SA Negotiation

**Key exam concept:** For two routers to form an ISAKMP SA, the **policy parameters must match**. If R1 has policy 100 (3DES, group 2, SHA, lifetime 43200) and R2 has policy 100 (DES, group 1, SHA, lifetime 86400), they **will NOT match**.

**The negotiation process:** R1 sends its policy to R2. R2 compares against its own policies. If a match is found, that policy is used. If no match → SA fails.

---

# UNIT 5: Network Address Translation — NAT (Week 11)

## 5.1 What is NAT?

**Core Concept:** NAT translates **private IPv4 addresses** to **public IPv4 addresses** and vice versa. It allows networks using private addresses internally to communicate with the Internet.

**Primary purpose:** Conserve public IPv4 addresses.

**Where it operates:** At the **border** of a stub network (edge router).

---

## 5.2 Private IP Address Ranges (RFC 1918)

| Class | Range | CIDR |
|-------|-------|------|
| A | 10.0.0.0 – 10.255.255.255 | 10.0.0.0/8 |
| B | 172.16.0.0 – 172.31.255.255 | 172.16.0.0/12 |
| C | 192.168.0.0 – 192.168.255.255 | 192.168.0.0/16 |

**How the professor expects it:** MCQ asking which IP ranges are private. Know all three ranges.

---

## 5.3 NAT Terminology

| Term | Meaning | Example |
|------|---------|---------|
| **Inside Local** | Source address as seen from INSIDE (private) | 192.168.10.10 |
| **Inside Global** | Source address as seen from OUTSIDE (public) | 209.165.200.226 |
| **Outside Global** | Destination address as seen from OUTSIDE | 209.165.201.1 |
| **Outside Local** | Destination address as seen from INSIDE | 209.165.201.1 (usually same) |

**Memory trick:**
- **Inside** = your network
- **Outside** = other network
- **Local** = as seen from inside
- **Global** = as seen from outside

---

## 5.4 How NAT Works

1. PC1 (192.168.10.10) sends packet to web server (209.165.201.1)
2. Router receives packet, reads source IP → creates NAT table entry (192.168.10.10 → 209.165.200.226)
3. Router sends packet with translated source address
4. Web server replies to 209.165.200.226
5. Router receives reply, checks NAT table, translates back (209.165.200.226 → 192.168.10.10)
6. Packet forwarded to PC1

---

## 5.5 Three Types of NAT

### 1. Static NAT
- **One-to-one** permanent mapping
- Private IP ↔ Public IP (always the same)
- Use case: Web servers that need a consistent public address
- Requires enough public addresses for all simultaneous users

### 2. Dynamic NAT
- **Many-to-many** from a pool
- Assigns public IPs from a pool on first-come, first-served basis
- When pool is exhausted, new connections are denied
- Requires enough public addresses for simultaneous sessions

### 3. PAT (Port Address Translation) / NAT Overload
- **Many-to-one** mapping
- Multiple private IPs share ONE public IP
- Uses **source port numbers** to distinguish sessions
- Most common type — used in home/office networks

**How the professor expects it:** Explain each type with examples. Know the difference between Static (1:1), Dynamic (pool), and PAT (many:1).

---

## 5.6 NAT Advantages and Disadvantages

### Advantages:
1. Conserves legally registered (public) addresses
2. Provides address multiplexing (PAT)
3. Increases connection flexibility
4. Consistency for internal addressing
5. Allows easy change to new public addressing
6. **Hides internal IP addresses** (security benefit)

### Disadvantages:
1. **Increases forwarding delays** (translation overhead)
2. **End-to-end addressing is lost** (breaks some protocols)
3. **End-to-end traceability is lost** (harder to track)
4. **Complicates tunneling protocols** (e.g., IPsec)
5. Can **disrupt services** that require incoming connections or use stateless protocols (UDP)

**How the professor expects it:** Open-ended: "Explain advantages and disadvantages of NAT."

---

# UNIT 6: Wireless Security (Week 12)

## 6.1 Types of Wireless Networks

| Type | Full Name | Coverage | Technology |
|------|-----------|----------|------------|
| **WPAN** | Wireless Personal Area Network | <10m | Bluetooth |
| **WLAN** | Wireless Local Area Network | Building | IEEE 802.11 (WiFi) |
| **WMAN** | Wireless Metropolitan Area Network | City | WiMAX |
| **WWAN** | Wireless Wide Area Network | Countries | 4G/5G/Satellite |

---

## 6.2 Wireless Network Vulnerabilities

1. **Shared media** — Packets are accessible to all (can be sniffed, hijacked)
2. **Signal blockage** — Electromagnetic waves blocked by metal/water, can be jammed
3. **No definite borders** — Signals extend beyond physical boundaries
4. **No fixed points** — Hard to pinpoint attacker's location

---

## 6.3 Types of Wireless Attacks

### Reconnaissance Attacks:
- Packet sniffers, ping sweeps, port scans

### Access Attacks:
- Password attacks, trust exploitation, man-in-the-middle

### Denial of Service Attacks:
- Single-message DoS, flooding DoS, distributed DoS, signal jamming

---

## 6.4 WLAN Attacks

| Attack | Description |
|--------|-------------|
| **WAR Driving/Walking** | Scanning for open wireless networks using a device |
| **RF Interference** | Flooding the RF spectrum to disrupt WLAN |
| **Evil Twin** | Rogue AP that **mimics** a legitimate AP — users connect to it unknowingly |
| **Rogue Access Point** | Unauthorized AP installed on a secure network, bypasses firewall security |

**Countermeasure:** Use monitoring tools (wireless protocol analyzers) to detect rogue APs.

---

## 6.5 Bluetooth Attacks (WPAN)

| Attack | Description |
|--------|-------------|
| **Bluejacking** | Sending unsolicited messages to Bluetooth devices (annoying, not harmful) |
| **Bluesnarfing** | Unauthorized access to data stored on a Bluetooth device (steals data) |
| **Bluebugging** | Attacker connects and executes commands on target device without owner's knowledge |
| **Blueborne** | Exploits stack buffer overflow to hijack Bluetooth connections and gain control |

---

## 6.6 WEP (Wired Equivalent Privacy)

**Core Concept:** WEP was the original WLAN security standard. It provides confidentiality using a shared secret key.

**How WEP works:**
1. Calculate **ICV** (Integrity Check Value) using CRC on plaintext
2. Generate random 24-bit **IV** (Initialization Vector)
3. Combine IV + Secret Key → RC4 generates a **keystream**
4. XOR keystream with plaintext → **ciphertext**
5. Prepend IV to ciphertext (so receiver can decrypt)

**WEP Weaknesses:**
1. **Key length too short** (64-bit or 128-bit)
2. **IV too short** (24-bit) → only ~16 million possible values
3. **Same IV + same key = same keystream** (collision attack)
4. **IV is sent unencrypted** (prepending)
5. Tools like **AirSnort/Aircrack-ng** can crack WEP in ~5-10 million packets (under 1 second)

---

## 6.7 WPA and WPA2

### WPA (Wi-Fi Protected Access)
- Replaces WEP's key with **TKIP** (Temporal Key Integrity Protocol) — creates per-packet keys to prevent collision
- PSK not used for encryption directly — used as starting point for key generation
- Replaces CRC with **MIC** (Message Integrity Check) for integrity

### WPA2 (Wi-Fi Protected Access 2)
- Uses **AES** (Advanced Encryption Standard) instead of RC4
- Key lengths: 128, 192, or 256 bits
- Much stronger than WPA

**How WPA/WPA2 address WEP weaknesses:**
- Longer keys (128+ bits vs WEP's short keys)
- Per-packet keys (TKIP) prevent IV collision
- AES encryption (WPA2) is much stronger than RC4
- MIC replaces CRC for integrity

---

## 6.8 WLAN Standards (802.11)

| Standard | Max Speed | Frequency | Backward Compatible |
|----------|-----------|-----------|---------------------|
| 802.11a | 54 Mbps | 5 GHz | No |
| 802.11b | 11 Mbps | 2.4 GHz | No |
| 802.11g | 54 Mbps | 2.4 GHz | 802.11b |
| 802.11n | 600 Mbps | 2.4/5 GHz | 802.11b/g |
| 802.11ac | 1.3 Gbps | 2.4/5.5 GHz | 802.11b/g/n |
| 802.11ad | 7 Gbps | 2.4/5/60 GHz | 802.11b/g/n/ac |

---

## 6.9 WWAN — WiMAX

**Core Concept:** WiMAX (Worldwide Interoperability for Microwave Access) provides wide-area wireless broadband.

- Range: **50 km** radius from base station
- Speed: **70 Mbps** (theoretical), 144 Mbps downlink / 35 Mbps uplink
- Coverage: Up to **8,000 km²**
- Line-of-sight NOT required

**WiMAX Security Issues:**
- PKM authentication flaw → susceptible to **man-in-the-middle attacks**
- Management frames not encrypted → info leakage
- Legacy management frames can disconnect legitimate stations
- Physical layer DoS attacks

---

# UNIT 7: Intrusion Detection and Prevention Systems (Week 13)

## 7.1 IDS vs IPS

| Feature | IDS (Intrusion Detection System) | IPS (Intrusion Prevention System) |
|---------|----------------------------------|-----------------------------------|
| **Mode** | Passive (monitors copies of traffic) | Active (inline, all traffic passes through) |
| **Action** | **Alerts/logs only** | **Stops attacks** + alerts/logs |
| **Impact on network** | No latency | Some latency |
| **If sensor fails** | No impact | Network affected |
| **Interface** | Promiscuous (copy of traffic) | Inline (traffic flows through) |

**How the professor expects it:** Know the difference. IDS = passive, alerts only. IPS = active, inline, can block.

---

## 7.2 IPS Signatures

**Core Concept:** A signature is a set of rules that IDS/IPS uses to detect intrusive activity (DoS attacks, worms, viruses, etc.).

**Signature Attributes:**
1. **Type** — Atomic or Composite
2. **Trigger (alarm)** — What triggers the signature
3. **Action** — What happens when triggered

### Signature Types:
| Type | Description |
|------|-------------|
| **Atomic** | Single packet, single event. No state information needed. Simplest form. |
| **Composite** | Multiple packets/events across multiple hosts. Requires state information. Has an **event horizon** (time window to maintain state). |

**How the professor expects it:** "An IPS sensor detects the string 'confidential' across multiple packets in a TCP session. What type?" → Pattern-based detection trigger, Composite signature type.

---

## 7.3 Four Types of Signature Triggers

| Trigger | How it works | Pros | Cons |
|---------|-------------|------|------|
| **Pattern-based** (Signature-based) | Searches for specific pre-defined patterns in traffic | Easy config, fewer false positives | Can't detect unknown attacks, signatures need updating |
| **Policy-based** (Behavior-based) | Defines suspicious behaviors based on historical analysis | Can detect unknown attacks, simple | Generic output, policy must be created |
| **Anomaly-based** (Profile-based) | Defines "normal" activity, flags deviations | Can detect unknown attacks, easy config | Hard to profile large networks, profile must be updated |
| **Reputation-based** | Tracks reputation scores of domains/IPs | Dynamic, can detect unknown attacks | Difficult to profile, policy must be created |

---

## 7.4 Alarm Types (Tuning)

| | Attack Traffic | Normal Traffic |
|---|---|---|
| **Alarm Generated** | ✅ **True Positive** (correct) | ❌ **False Positive** (wrong) |
| **No Alarm Generated** | ❌ **False Negative** (dangerous!) | ✅ **True Negative** (correct) |

**Key definitions:**
- **False Positive:** Alarm generated for normal traffic → Need to **tune the alarm** to reduce these
- **False Negative:** No alarm for attack traffic → **Most dangerous** — means attacks go undetected. Must ensure IPS doesn't produce these.

**How the professor expects it:** Given scenarios, categorize as True Positive/False Positive/True Negative/False Negative.

---

## 7.5 IPS Signature Actions

When a signature triggers, it can perform:

| Category | Action | Description |
|----------|--------|-------------|
| **Alert** | Produce alert | Writes event to Event Store |
| | Produce verbose alert | Includes encoded packet dump |
| **Log** | Log attacker packets | Starts IP logging on attacker |
| | Log pair packets | Logs attacker + victim pair |
| | Log victim packets | Logs victim traffic |
| **Drop/Prevent** | Deny attacker inline | Drops current + future packets from attacker (sliding timer) |
| | Deny connection inline | Drops current + future packets on this TCP flow |
| | Deny packet inline | Drops current packet only |
| **Reset** | Reset TCP connection | Sends TCP resets to terminate the flow |
| **Block** | Request block connection | Requests blocking device to block this connection |
| | Request block host | Requests blocking device to block this attacker host |

---

## 7.6 Implementing Cisco IOS IPS (5 Steps)

1. **Download** IOS IPS files (signature package + public crypto key from cisco.com)
2. **Create IPS directory** in flash:
   ```
   R1# mkdir ips
   ```
3. **Configure IPS crypto key** (paste the RSA public key text at config prompt)
4. **Enable IOS IPS:**
   ```
   R1(config)# ip ips name IOSIPS
   R1(config)# ip ips config location flash:ips
   R1(config)# ip http server
   R1(config)# ip ips notify sdee
   R1(config)# ip ips notify log
   ```
5. **Load signature package:**
   ```
   R1# copy ftp://cisco:cisco@10.1.1.1/IOS-S376-CLI.pkg idconf
   ```

### Configure Signature Categories:
```
R1(config)# ip ips signature-category
R1(config-ips-category)# category all
R1(config-ips-category-action)# retired true    ← retire all first
R1(config-ips-category-action)# exit
R1(config-ips-category)# category ios_ips basic
R1(config-ips-category-action)# retired false   ← unretire basic
R1(config-ips-category-action)# exit
R1(config-ips-category)# exit
```

### Apply IPS to Interface:
```
R1(config)# interface GigabitEthernet 0/1
R1(config-if)# ip ips IOSIPS in
R1(config-if)# ip ips IOSIPS out
```

**Retired vs Unretired:**
- **Retired** = signature NOT compiled into memory (not used)
- **Unretired** = signature IS compiled and used for scanning

---

## 7.7 SDEE and Logging

- **SDEE** (Security Device Event Exchange) — protocol for exchanging IPS messages
- SDEE notification must be **explicitly enabled**: `ip ips notify sdee`
- HTTP server must be enabled: `ip http server` (SDEE works over HTTP)
- Logging is enabled by default: `ip ips notify log`
- Both can be used simultaneously

---

## 7.8 Signature File Updates

- New signatures published by Cisco: **biweekly** (normal), **within hours** (severe)
- Each update includes **all previous signatures** plus new ones
- Signature file naming: IOS-S361-CLI.pkg (includes all of S360 + new)
- Download from **CCO** (Cisco Connection Online) — requires valid CCO login

---

## 7.9 Verifying IPS

| Command | Shows |
|---------|-------|
| `show ip ips signature count` | Signature counts (total, enabled, retired, compiled) |
| `show ip ips all` | Full IPS configuration status |
| `show ip ips configuration` | IPS config details |
| `show ip ips interfaces` | Which interfaces have IPS rules |
| `show ip ips statistics` | Packet statistics (audited packets) |

---

## 7.10 Modifying Signatures

**Retire an individual signature:**
```
R1(config)# ip ips signature-definition
R1(config-sigdef)# signature 6130 10
R1(config-sigdef-sig)# status
R1(config-sigdef-sig-status)# retired true
```

**Change signature actions:**
```
R1(config)# ip ips signature-definition
R1(config-sigdef)# signature 6130 10
R1(config-sigdef-sig)# engine
R1(config-sigdef-sig-engine)# event-action produce-alert
R1(config-sigdef-sig-engine)# event-action deny-packet-inline
R1(config-sigdef-sig-engine)# event-action reset-tcp-connection
```

**Signature 6130 10** → Signature number 6130, sub-signature ID 10.

---

# QUICK REFERENCE: Key Exam Facts

| Fact | Answer |
|------|--------|
| OSPF default AD | 110 |
| OSPF Hello interval (Ethernet) | 10 seconds |
| OSPF Dead interval (Ethernet) | 40 seconds |
| OSPF authentication types | Null (Type 0), Simple (Type 1), MD5 (Type 2) |
| Standard ACL number range | 1–99 |
| Extended ACL number range | 100–199 |
| Standard ACL placement | Closest to destination |
| Extended ACL placement | Closest to source |
| Implicit ACL at end of every ACL | deny any |
| AH protocol number | 51 |
| ESP protocol number | 50 |
| IKE port | UDP 500 |
| IPsec that provides encryption | ESP |
| NAT private IP ranges | 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 |
| PAT uses what to distinguish sessions | Port numbers |
| WEP IV length | 24 bits |
| WPA2 encryption algorithm | AES |
| WEP encryption algorithm | RC4 |
| IDS mode | Passive (promiscuous) |
| IPS mode | Active (inline) |
| False Positive | Alarm for normal traffic |
| False Negative | No alarm for attack traffic (most dangerous) |

---

*Study this guide unit by unit. For each unit, make sure you can:*
1. *Define every term*
2. *Explain the concept in your own words*
3. *Write out configuration commands from memory*
4. *Answer "why does this matter" and "how does it connect to other topics"*
5. *Given a scenario, identify what's wrong and how to fix it*
