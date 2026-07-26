# IT2515 Operating System & Security — Complete Study Guide
## Weeks 7–13 | 5 Structured Questions + 1 Long Question | 40 Minutes

> **How to use this guide:** Study unit by unit, top to bottom. Every topic, term, and concept mentioned in the course handouts is covered here. Pay special attention to **bold terms** — these are high-probability exam terms.

---

# UNIT 1: Introduction to Directory Services (Week 7)
*Source: Chap06, Tutorial 6, Practical 7*

---

## 1.1 What is a Directory Service?

**Core Concept:** A directory service is a centralized database that maps network resources (users, printers, folders, devices) to their network addresses. Think of it like a phone book for your entire network — everyone looks up resources in one place instead of searching manually.

**Key Properties:**
- Each network resource exists as an **object**
- Each object has a collection of **attributes** (properties describing it)
- All objects belong to a **namespace** or **domain**
- Each object must be **uniquely identified** within its namespace
- Often called an **information store**

**Why it matters:** Without directory services, user credentials must be synced manually across machines (tedious, error-prone), password changes can't sync in real time, no seamless roaming profiles, and resource sharing (files, printers) is very difficult.

---

## 1.2 History and Protocols

**Before X.500 (1980s):**
- Each directory service needed its own custom protocol
- Examples: DNS (Domain Name Service), Windows NT domain, NIS (Network Information Service)

**X.500 Directory Access Protocol:**
- Developed by ITU/ISO in the 1980s
- First open standard for directory access
- All modern directory services derive from or are influenced by X.500

**After X.500:**
- **Active Directory** (Microsoft)
- **Apache Directory Server**
- **Open LDAP**

**Key Protocol — LDAP (Lightweight Directory Access Protocol):**
- Makes the information store accessible from many different operating systems
- This is what allows cross-platform directory access

---

## 1.3 Key Properties of Directory Services

| Property | Explanation |
|----------|-------------|
| Single point of access | All users locate IT resources/services from one place |
| Distributed backend | Database can be stored on different machines |
| Not transactional | Cannot handle high volume of data edits — but this is fine because directory data is stable and rarely changes |
| Extensible | Can accommodate new object types and attributes as needs change |
| Searchable | Users/admins can search from various locations |
| Cross-platform | Achieved via LDAP |

---

## 1.4 Active Directory Domain Services (AD DS)

**What it is:** Microsoft's directory service implementation, available since Windows Server 2008. Only available on Windows Server OS. Supports LDAP.

**Core Components:**
1. **Domain Controller (DC)** — Handles network resource authentication/authorization, Group Policy management and enforcement, Kerberos authentication service
2. **DNS** — Domain Name Service (required for AD to function)

---

## 1.5 AD Structure

**AD Objects are grouped into:**
- **Resources** — Printers, shared folders, etc.
- **Security Principals** — Users, groups, computer accounts (assigned a **Security Identifier / SID**)
- **AD Schema** — Defines all objects and their attributes

**Database access methods:** GUI application (ADUC), LDAP, or ADSI Editor

---

## 1.6 Domains, Trees, and Forests

These are the **logical divisions** of an AD network:

**Domain:**
- Logical grouping of network objects that share the **same AD database**
- The basic building block of AD

**Tree:**
- Collection of one or more domains within a **single contiguous namespace**
- Linked together with **transitive trust hierarchy**
- Example: `example.com` → `sales.example.com` → `tech.example.com`

**Forest:**
- Collection of one or more trees
- Share a common: **global catalog**, **directory schema**, **logical structure**, **directory configuration**
- Represents the **security boundary** of all accessible objects

**Global Catalog:**
- Read-only catalog of all objects within a forest
- Contains only a **small subset** of object attributes
- Used for fast/efficient object searches within a forest
- Actual domain still consulted for full object detail

**Exam tip:** Know the hierarchy: Forest → Trees → Domains. Understand that a forest is the security boundary.

---

## 1.7 Organizational Units (OUs) vs Containers

| Feature | OU | Container |
|---------|-----|-----------|
| Can contain objects | ✅ | ✅ |
| Can link to GPOs | ✅ | ❌ |
| Can contain other OUs | ✅ | ❌ |
| Can delegate admin rights | ✅ | ❌ |
| Icon in ADUC | Folder with book | Plain folder |

**Default OU created when AD is first installed:** Domain Controllers OU

**Domain Controllers OU:**
- Created by default
- As more DCs are added, their objects appear here
- Has a default GPO linked to it (ensures consistent DC configuration)
- **Not recommended** to move DC objects away — may cause DC to misbehave

---

## 1.8 AD Database Partitions (Naming Contexts)

| Partition | What it contains | Replicated to |
|-----------|-----------------|---------------|
| **Schema** | Object and attribute definitions of the forest | All DCs in the forest |
| **Configuration** | Physical structure and configuration of the forest | All DCs in the forest |
| **Domain** | All domain objects (users, groups, GPOs, computers) | Only DCs of the **same domain** |

- Replication is **automatically configured** when a server is promoted to DC
- Changes are **pulled** (not pushed) to other DCs via **change notification**

**Exam tip:** Schema and Configuration replicate forest-wide. Domain partition replicates only within the same domain.

---

## 1.9 Physical DC Implementation

- **Minimum:** 1 DC per domain
- **Recommended for redundancy:** 2+ DCs per domain (peer domain controllers)

---

## 1.10 AD Global Catalog (GC)

**Problem:** Domain partition objects only replicate within the same domain. How do we access objects from another domain in the same forest?

**Solution: Global Catalog**
- A subset of domain objects is replicated to all DCs in the forest configured as GC
- Provides a **summary** of all objects in the forest
- Only **selected attributes** are replicated
- Viewable via ADSIEdit

---

# UNIT 2: AD Object Management & GPOs (Week 8)
*Source: Chap07, Tutorial 7, Practical 8*

---

## 2.1 Active Directory Objects

| Object Type | Description |
|-------------|-------------|
| **User** | First/last name, login credentials |
| **Contact** | Contact info for people associated with org (e.g., supplier) |
| **Printer** | Pointer to a printer on the network |
| **Computer** | Info about computers on the network |
| **Shared Folder** | Pointer to a shared folder on a computer |
| **Group** | Collection of users, computers, contacts, or other groups |
| **Container** | Can hold other AD objects **except OUs** |
| **OU** | Special container — can link to GPOs, contain other objects |
| **Domain** | Group of users/computers/resources with certain rules |
| **Domain Controller** | Info about DCs (owner, DNS name, pre-Win2000 name) |
| **Site Objects** | Manage and facilitate AD replication |
| **Builtin** | Contains built-in local groups |
| **Foreign Security Principals** | Shows trust relationships with other domains |

---

## 2.2 AD Users and Computers (ADUC)

**What it is:** GUI application for AD Object Management — create, manage, modify, delete AD objects.

**User Object Mandatory Attributes:**
- **cn** — Common Name
- **SAMAccountName** — Security Account Manager Name (supports older Windows clients)
- Attributes must be **unique across the domain**

**Security Identifiers (SID):**
- All AD security principal objects get a unique SID at creation
- AD uses SIDs for security management
- **Critical rule:** Deleting and re-creating an object with the same attributes does NOT work — the SID will be different!

---

## 2.3 Advanced Features of ADUC

**Enable:** ADUC → View → Advanced Features

**What it unlocks:**
1. **Viewing/editing object attributes** — Right-click object → Properties → Attribute Editor tab
2. **Object deletion protection** — Object tab → uncheck "Protect object from accidental deletion"
3. **Searching for objects** — Right-click container → Find → specify object type and container

---

## 2.4 Disabling vs Deleting User Accounts

**Disable:** For inactive users (on leave, etc.). Right-click → Disable Account.

**Best practice for ex-employees:** Disable first for a period, then delete later. This gives time to transfer data, revoke access gradually, etc.

---

## 2.5 Workgroup vs AD Domain

| Feature | Workgroup | AD Domain |
|---------|-----------|-----------|
| Network type | Peer-to-peer | Client-server |
| Central authentication | ❌ | ✅ (Domain Controller) |
| Each computer functions as | Both client and server | Client (DC handles server role) |
| Remote resource access | Requires account setup on each node | Centralized permissions |
| Best for | ≤15 computers | Enterprise environments |
| Password sync | Cannot sync automatically | Synced via AD |

---

## 2.6 Security Account Manager (SAM)

- **Local database** holding all local user and group accounts
- Authenticates local user logins
- Used in Windows Workgroups too
- Location: `C:\Windows\System32\config`
- Password hashes stored in `HKEY_LOCAL_MACHINE\SAM`
- **Cannot be accessed directly** while OS is running
- Before DC promotion: local 'administrator' credentials stored in SAM → used for **Directory Services Restore Mode (DSRM)**
- After DC promotion: administrator credentials move to AD

---

## 2.7 AD Account Group Types

**Distribution Groups:**
- Used **only with email applications**
- No SID → cannot be given permissions
- Cannot be used for security purposes

**Security Groups:**
- Security principal with SID
- Can be given permissions
- Can be email-enabled
- **Default group type** for newly created groups

---

## 2.8 Security Group Scoping

| Scope | Resource Access |
|-------|----------------|
| **Local** | Local computer resources only |
| **Domain Local** | Local domain resources only |
| **Global** | Resources within the forest |
| **Universal** | Resources within the forest |

---

## 2.9 AD Default Security Groups

| Group | Description |
|-------|-------------|
| **Enterprise Admins** | Member of Administrators group in EVERY domain of the forest. Complete admin rights to all DCs. Use with care! |
| **Schema Admins** | Full control of the AD schema |
| **Administrators** | Complete access to all resources on a machine |
| **Domain Admins** | Member of Administrators group of ALL machines in the domain. Admin rights to everything in the domain |
| **Domain Users** | All non-admin AD user accounts are automatically members. Access can be restricted based on this group |

---

## 2.10 Special Identities

- **Controlled by the OS** — cannot be created or deleted
- Exist even without AD Domain services
- View via ADSIEdit → Configuration partition → `cn=WellKnown Security Principals`

| Identity | Meaning |
|----------|---------|
| **Anonymous Login** | Any unauthenticated access |
| **Everyone** | Authenticated users + Guest account |
| **Interactive** | Local users accessing local computer resource |
| **Network** | Users accessing a network resource |
| **Creator Owner** | Security principal that created the object |

---

## 2.11 Computer Accounts

- Computers have AD accounts with SAMAccountName and password
- Password stored as **LSA (Local Security Authority) secret**
- Password **changed every 30 days** with the DC
- Creates a **secure channel** between computer and DC

**When the secure channel breaks:**
- Computer reinstallation (new SID/password)
- Restoring from very old backup/snapshot
- LSA secret out of sync with DC

**Resetting:** ADUC → right-click computer → Reset Account → re-join client to domain

---

## 2.12 AD Recycle Bin and Tombstones

**Tombstones:**
- When AD object is deleted → becomes a **tombstone object** → moved to **"Deleted Objects"** container
- After **180 days** by default → tombstone is fully removed
- Purpose: ensures correct replication of delete across peer DCs; ensures correct state after AD restore
- Restoration possible before full removal (preserves SID)

**AD Recycle Bin:**
- **Not enabled by default**
- Enable via AD Administrative Center
- Allows easier recovery of deleted objects

---

## 2.13 Group Policy Objects (GPOs) — Basics

**Purpose:** Reduce administrative burden by centrally controlling/configuring settings on Windows computers.

**Two Types:**
| Type | Scope |
|------|-------|
| **Local** | Applicable only to the local computer |
| **Domain** | Applicable to all computers/accounts in the domain (Active Directory GPOs) |

---

## 2.14 Local Group Policies

Multiple LGPOs can exist, each applied at different levels:
1. **Local Computer Policy** — applies to computer + everyone who logs on
2. **Administrators Local Group Policy** — applies to built-in Administrators group members
3. **Non-Administrators Local Group Policy** — applies to non-Administrators
4. **User-specific policies** — applies to specific local users

**Local GPO Editor:**
- Via MMC (Microsoft Management Console) with Group Policy Editor snap-in (manages all LGPO types)
- Via `gpedit.msc` command (only manages Local Computer Policy)

---

## 2.15 GPO Structure

GPOs are divided into two areas:
- **Computer Configuration** — applies when computer starts
- **User Configuration** — applies when user logs on

Each area contains:

| Node | Computer Config | User Config |
|------|----------------|-------------|
| **Software Settings** | Software Installation | Software Installation |
| **Windows Settings** | Name Resolution Policy, Scripts, Security Settings, Policy-based QoS | Scripts, Security Settings, Policy-based QoS |
| **Administrative Templates** | Control Panel, Network, Printers, System, Windows Components, All Settings | Control Panel, Desktop, Network, Shared Folders, Start Menu/Taskbar, System, Windows Components, All Settings |

---

## 2.16 Administrative Templates

Settings used by admins to modify the registry via policies.

| Feature | ADM (XP and earlier) | ADMX/ADML (Present) |
|---------|---------------------|---------------------|
| Structure | Groups complex settings into chunky files | Splits into small, easy-to-handle files |
| Storage | Higher | Lower |
| Syntax | ADM syntax | XML syntax |
| Default location | `C:\Windows\inf` | `C:\Windows\policyDefinitions` |
| Storage in GPO | Added to GPO contents | From computer performing GPO admin; centralized after central store |

---

## 2.17 Domain Group Policy

- Applies to **all domain-joined** computers and user accounts
- Editor only found on the DC computer
- Found under **Tools → Group Policy Management**
- Centrally stored on AD Domain server

---

## 2.18 GPO Activation

GPOs are activated when:
1. Computer starts/boot up
2. `gpupdate` command issued
3. User logon

**Auto-refresh:** Every **90 minutes** with a random **30-minute offset** (prevents overloading DC)

Some settings only apply at startup/logon:
- Automated software installation
- Drive mappings
- Startup/logon scripts

---

## 2.19 GPO Processing Order (CRITICAL EXAM TOPIC)

Processing order (top to bottom, last wins):
1. **Local** (lowest precedence)
2. **Site**
3. **Domain**
4. **Organizational Unit** (highest precedence)

**Within the same level with multiple GPOs:** Processed by **reversed link order** — GPO with link order number **1** has highest precedence.

**Sub-OUs:** GPOs at the highest level processed first, child OUs processed last (child OU GPOs have highest precedence — they are closest to the user/computer object).

**Exam tip:** "Last writer wins" — the GPO closest to the user/computer object takes precedence. Link order 1 = highest precedence within the same OU.

---

## 2.20 GPO Inheritance and Blocking

**Default behavior:** GPOs applied to parent containers (domain, site, OU) are **inherited** by child containers.

**Blocking inheritance:** Can be disabled on a child OU — stops all parent GPOs from being inherited.

---

## 2.21 GPO Enforcement

- Enforcing a GPO means its settings **take precedence over child object settings**
- **Works even if inheritance is blocked!**
- An enforced GPO overrides everything

**Exam tip:** Enforcement > Block Inheritance. An enforced parent GPO beats a child OU that has blocked inheritance.

---

## 2.22 GPO Troubleshooting with RSoP

**Resultant Set of Policies (RSoP):**
- Report of all settings **after** GPOs have been processed
- Two ways to activate:
  1. `rsop` command (must be admin account)
  2. MMC via RSoP snap-in (more flexible — can simulate on any container/user/computer)
- Also: `gpresult /v` for text-based report

---

# UNIT 3: Securing AD Domain Services (Week 9)
*Source: Chap08, Tutorial 8, Practical 9*

---

## 3.1 Motivations for Securing AD

AD is a **prime target for cyber attacks**. Risks include:
- Network security threats
- Authentication attacks
- Elevation of privileges
- DoS attacks
- OS/system/service/application attacks
- Operational risks
- Physical security threats

---

## 3.2 Securing DCs via GPOs

- AD domains typically have 2+ DCs for redundancy
- Individually securing each DC is administratively heavy
- **Solution:** Use GPO for consistent security configuration

---

## 3.3 Default Domain Policy vs Default Domain Controller Policy

These are the **2 default GPOs** activated when any DC is first started after installation:

| GPO | Scope |
|-----|-------|
| **Default Domain Policy** | Applies to **ALL objects** in the AD domain — users, computers, DCs, servers |
| **Default Domain Controller Policy** | Links **only** to the Domain Controllers OU. Settings apply only to DCs |

**Exam tip:** Don't confuse these two! Default Domain Policy = everyone. Default Domain Controller Policy = DCs only.

---

## 3.4 GPO Settings for Enhanced Security

Located in: `Computer Configuration\Policies\Windows Settings\Security Settings`

- **Account policies** — password and account lockout
- **Local policies** — local auditing, user account rights, security options
- **Event log configuration**
- **Windows Firewall with Advanced Security**

Additional settings:
- **Restricted Groups** — locks group editing by other AD tools. Controls group membership.
- **Systems Services** — disable unnecessary services (reduces attack surface)
- **Advanced Audit Policy** — granular audit settings tracked in event logs

---

## 3.5 Planning for Secure AD Services

1. **Secure user accounts/passwords** — complex password policy
2. **Secure groups with elevated permissions** — limit and review membership
3. **Audit security events** — enable event logging for authentication and resource access
4. **Establish deprovisioning/cleanup** — review accounts/memberships periodically; decommissioned computers should not authenticate; scrub hard disks
5. **Secure client computers** — regular password changes; reset computer accounts if reported lost

---

## 3.6 Securing Domain Controllers (Physical + Logical)

- **Physical security:** CCTV monitoring, card access
- **Read-only Domain Controllers (RODC)** where possible
- **BitLocker** on DC disk volumes (drive encryption)
- **Monitor hot swap disk systems** — disks can be easily swapped = data theft
- **Store backups in secure locations**

---

## 3.7 Read-Only Domain Controllers (RODC)

- Contains AD data in **read-only mode** — cannot edit AD data
- Used in **remote office sites** where secured facilities are challenging
- Contains all AD objects and attributes **except security-related ones by default**
- All authentication requests forwarded to normal DCs
- **Credential caching** can be configured — then RODC can authenticate domain users
- If RODC is compromised/stolen, security info is NOT exposed (except cached credentials)

---

## 3.8 RODC Password Replication Policy

Determines which users' credentials get cached on the RODC.

**Domain-wide policy:**
| Group | Behavior |
|-------|----------|
| **Allowed RODC Password Replication** | Members' credentials cached on any domain RODCs. By default: no members |
| **Denied RODC Password Replication** | Members' credentials NEVER cached on RODCs. By default: Domain Admins, Enterprise Admins, Group Policy Creator Owners |

**RODC-specific policy:** Configured via specific RODC properties. Contains both domain-wide allowed/denied groups plus RODC-specific additions.

---

## 3.9 Account Security Features — Password Policies

| Policy | Description |
|--------|-------------|
| **Enforce password history** | How many previous passwords a user cannot reuse |
| **Maximum password age** | Max time before required password change |
| **Minimum password age** | Min time before password can be changed (must be < max) |
| **Minimum password length** | Minimum characters |
| **Password complexity** | Cannot contain username; ≥6 chars; must contain chars from 3 of 4 groups (uppercase, lowercase, numeric, special) |

---

## 3.10 Account Lockout Policies

| Policy | Description |
|--------|-------------|
| **Account lockout duration** | Minutes account is locked. **Value 0** = admin must manually unlock |
| **Account lockout threshold** | Failed attempts before lockout. **Value 0** = never locked |
| **Reset account lockout counter after** | Minutes before failed login counter resets to 0 |

---

## 3.11 Auditing Authentication Events

**Two types of logon events:**

| Event Type | Where Generated | When |
|-----------|----------------|------|
| **Account logon events** | On the DC | User logs in with domain account (auth performed on DC) or local accounts logon |
| **Logon events** | On the client machine | User login not authenticated locally (forwarded to DC); also when domain user accesses network resources (e.g., shared folders) |

**Enabling:** Via GPO → `Security Settings\Local Policies\Audit Policy` → select Success/Failure
**Reviewing:** Event Viewer

---

## 3.12 AD Database Components

**3 Database Partitions:**

| Partition | Contents |
|-----------|----------|
| **Domain** | GPOs, users, groups, computers |
| **Configuration** | Forest/domains info, physical topology, sites, subnets, services |
| **Schema** | AD object class and attribute definitions |

**File-level components** (default location: `%SystemRoot%\NTDS`):

| File | Purpose |
|------|---------|
| **Ntds.dit** | Main AD DS database file |
| **Edb*.log** | Transaction logs |
| **Edb.chk** | Database checkpoint file |
| **Edbres00001.jrs / Edbres00002.jrs** | Reserve log files (if main DB runs out of space) |

---

## 3.13 NTDSUtil.exe

Used for AD database maintenance:
- **Offline defragmentation**
- **Create and mount snapshots**
- **Move database file**
- **Clean database metadata** (DC removal/demotion while disconnected)
- **Destroy sensitive information**
- **Reset DSRM password** (`Set dsrm` command)

---

## 3.14 AD Domain Server States

| State | Description |
|-------|-------------|
| **AD DS Started** | Normal operation |
| **AD DS Stopped** | Cannot perform system state/backup restoration. Used for offline defrag and DC updates. Services not depending on AD DS (e.g., DHCP) can continue |
| **DSRM** | DC is offline. Another DC should serve DS. Must be in this mode for system state/backup restoration |

---

## 3.15 AD Snapshots

- Exact copy of a historical state of DS at time of snapshot
- Create/mount via `ntdsutil`
- View/read-only examination only
- **Cannot restore AD data from snapshots!**
- Used for **verifying AD data** only

---

## 3.16 Windows Domain Server Backup

**Tool:** MMC console with wbadmin snap-in

**Backup types:**
- Full server backup (all volumes)
- Selected volumes
- Specific items (folders, system state)

**Restore:** System state using DSRM → roll back to specific point in time. Can recover individual files/folders/volumes.

**Backup Automation:**
- Included Backup Scheduler
- Can be once or more per day
- Archive to another disk volume or shared network folder

---

## 3.17 AD Domain Server Recovery

**Entering DSRM:**
- PowerShell: `bcdedit /set safeboot dsrepair` → `shutdown –t 0 /r`
- Or press F8 on OS load screen

**Two recovery types:**

| Type | Process |
|------|---------|
| **Non-authoritative (normal)** | Restore DC to previously known state. DC then **updates from partner DCs** |
| **Authoritative** | Restore DC to previously known state. **Mark specific objects as authoritative** (confirmed as only good copies). DC sends authoritative updates to peers; receives non-authoritative updates from peers |

---

# UNIT 4: Linux Advanced Security — SELinux & PAM (Week 10)
*Source: Chap09, Tutorial 9, Practical 10*

---

## 4.1 Linux File Permissions Revision

**Basic attributes:**
- **r** — readable
- **w** — writable
- **x** — execute/directory accessible

**Three permission sets:**
- **u** — user (owner) permission
- **g** — group permission
- **o** — others permission

**Format:** `rwxrwxrwx` → `u  g  o`

**Example:** `-rw-r--r--` = owner can read/write, group can read, others can read

**Access evaluation order:**
1. Check user owner → if match, apply user permissions (stop)
2. Check group owner → if match, apply group permissions (stop)
3. Apply others permissions

---

## 4.2 Process Owner

- Every Linux process runs with a **uid** (determined by who started the process)
- File access for processes is evaluated the same way as for users
- A process running as `userA` can only access files based on `userA`'s permissions

---

## 4.3 Discretionary Access Control (DAC)

- The **default access control mechanism** for all Linux
- The **owner of a resource decides** how it's shared
- Any process/user logged in as **root** → no DAC evaluation needed → **unconditional access**
- Root is the most powerful account under DAC

---

## 4.4 Mandatory Access Control (MAC)

- **Fine-grained mechanism** — security administrator defines what user/process can do
- **SELinux** is the MAC system for Linux
- Enforcement done by the **kernel**
- Governed by **security policy loaded at system start**

**Critical rule:** MAC cannot work alone — **DAC must still be active** as the default.
- DAC is evaluated **first**
- If DAC denies → MAC not evaluated
- If DAC allows → MAC is then evaluated

**MAC Evaluation Flowchart:**
```
Start → Is DAC allowed? 
  No → Access Denied
  Yes → Is MAC allowed?
    No → Access Denied
    Yes → Access Allowed
```

---

## 4.5 Motivations for SELinux

**Scenario 1:** Server process running as root is compromised → hacker inherits root UID → under DAC alone, entire system is compromised.

**Scenario 2:** System has sensitive data off-limits even to administrators. Under DAC with root access, admins can copy it.

**SELinux solves these** by adding a mandatory layer that even root cannot bypass without the proper security context.

---

## 4.6 SELinux Security Contexts

Labels applied to **everything** in the system (files, processes).

**Format:** `SELinux_user:role:type:level`

**Example:** `system_u:system_r:xserver_t:s0-s0:c0.c1023`

| Field | Convention | Description |
|-------|-----------|-------------|
| SELinux user | Ends with `_u` | Linux users mapped to SELinux users |
| Role | Ends with `_r` | RBAC attribute — intermediary between domains and SELinux users |
| Type | Ends with `_t` | Type Enforcement attribute — defines domain for processes |
| Level | Starts with `s`, categories start with `c` | Optional. MLS/MCS attribute |

**After DAC passes, security contexts are checked against the SELinux policy.**

---

## 4.7 Viewing Security Contexts

| Command | What it shows |
|---------|---------------|
| `ls -Z` | File security contexts |
| `ps -Z` | Process security contexts |
| `id -Z` | Current login user security context |

---

## 4.8 SELinux Security Policy

- Work in progress (ongoing development)
- Most distributions adapt from **reference policy** (https://github.com/SELinuxProject/refpolicy)
- Contains:
  - Access rules
  - Default security contexts for processes/files/login users
- Full policy modification is beyond the module scope

---

## 4.9 Default SELinux Enforcement — Type Enforcement

- Works on the **3rd field** (type) of the security context
- Compares subject (user/process) type vs object (file resource) type
- Policy consulted for access evaluation

**Example rule:**
```
allow system_t bin_t:file execute;
```
→ Allows subject with `system_t` to execute any file labelled `bin_t`

---

## 4.10 SELinux Configuration

**File:** `/etc/selinux/config` (persists across reboots)

```
SELINUX=enforcing|permissive|disabled
SELINUXTYPE=targeted|minimum|mls
```

---

## 4.11 SELinux Operating Modes

| Mode | Behavior |
|------|----------|
| **Enforcing** (Default for CentOS) | Policy active. Violations **logged AND disallowed** |
| **Permissive** | Policy active. Violations **logged but allowed**. Used for testing |
| **Disabled** | Policy inactive. Access control defaults to DAC only |

**Dynamically changing mode (temporary, until reboot):**
- `setenforce 0` → Permissive
- `setenforce 1` → Enforcing
- `getenforce` → check current mode

**Persistent changes:** Edit `/etc/selinux/config`

---

## 4.12 SELinux Enforcement Policy Types

| Type | Description |
|------|-------------|
| **Targeted** (Default for CentOS) | Selected processes protected. Not all processes have proper security contexts. View protected processes: `semanage module -l` |
| **Minimum** | Minimum processes protected (buggy!) |
| **MLS** | Multi Level Security (buggy!) |

---

## 4.13 Viewing Active SELinux Configuration

- `sestatus` — shows status, mount point, root directory, loaded policy, current mode, mode from config

---

## 4.14 SELinux Policy Constraints & Modification

The static policy can be slightly modified via:
1. **SELinux Booleans** — toggle-able policy options
2. **Customized Local Security Policy Modules** — custom rules for specific needs

**SELinux Troubleshooter GUI:**
- Available in GUI environments
- Alert window shows every SELinux access denied violation
- Offers instructions for remediation (custom LSM or Boolean settings)

---

## 4.15 Pluggable Authentication Module (PAM)

**What it is:** An API framework for authentication-related services.

**Why PAM exists:** Before PAM, every Linux application needing authentication had to develop its own system and database → complex, inconsistent, impossible to integrate OS password auth into 3rd-party apps.

**PAM provides:**
- Common authentication scheme for many applications
- Significant flexibility and control
- Single, fully-documented library for developers

---

## 4.16 PAM Architecture

```
Processes → Process-Related PAM Config Files → Auth-Specific PAM Modules
```

**Authentication flow example (SSHD):**
1. SSHD prompts for username/password → `libpam` auth call → `pam_unix` checks local account → result returned
2. SSHD asks "Is user allowed to connect?" → `libpam` account call → `pam_unix` checks account status → result returned
3. SSHD creates session → `libpam` session call → `pam_limits` restricts resources → credentials re-checked

---

## 4.17 PAM Configuration Files

- Located in: **`/etc/pam.d/`**
- Named after the process/service (e.g., `/etc/pam.d/sshd`, `/etc/pam.d/login`)
- Format: `module_interface  control_flag  module_name  module_arguments`
- Processed **top to bottom**

---

## 4.18 PAM Module Interfaces (4 Types)

| Interface | Purpose |
|-----------|---------|
| **auth** | Determines if user is who they claim to be (password, biometrics, etc.) |
| **account** | Determines if user is allowed to access the service (password expired, etc.) |
| **password** | Used for changing user passwords |
| **session** | Before/after authentication actions (mount home dir, logging, restrict services) |

**Note:** Not necessary to define all 4 in every PAM config file.

---

## 4.19 PAM Authentication Modules

- Binary files located in **`/usr/lib64/security`**
- Use `man` command to learn functionality (e.g., `man pam_access`)
- Module arguments also detailed in man pages

---

## 4.20 PAM Control Flags

| Flag | Behavior |
|------|----------|
| **required** | Module failure → interface failure, but PAM still calls remaining modules before denying |
| **requisite** | Module failure → **immediate** denial |
| **sufficient** | Failure is ignored. If succeeds AND no previous required modules failed → interface success, no more modules needed |
| **optional** | Result only significant if no other modules reference this interface |
| **include** | Include all lines of given type from specified config file |
| **substack** | Include all lines of given type from specified config file (like include but in a separate sub-stack) |

**Exam tip:** Know the difference between `required` (continues checking, denies at end) and `requisite` (stops immediately on failure).

---

## 4.21 Practical: Disabling Root Login via PAM

**For GUI login (gdm-password):**
Add as first auth line:
```
auth  required  pam_succeed_if.so user != root quiet_success
```
→ Root cannot login via GUI, but text console login still works.

**For SSH login (sshd):**
Same line in `/etc/pam.d/sshd`:
```
auth  required  pam_succeed_if.so user != root quiet_success
```

**For blocking multiple users:** Use `pam_listfile.so`:
```
auth  required  pam_listfile.so item=user sense=deny onerr=fail file=/etc/sshdUserList
```
Then create `/etc/sshdUserList` with blocked usernames.

---

# UNIT 5: GPO Delegation & Advanced Security (Practical 9 Specifics)
*Source: Practical 9*

---

## 5.1 GPO Delegation

**Purpose:** Selectively apply GPOs to specific users within an OU.

**How it works:**
1. Create GPO on OU (e.g., "Disable Powershell" on ITAdministrators OU)
2. Go to GPO → Delegation tab → Add user
3. Click Advanced → Select user → **Deny** "Apply group policy" permission
4. That user is exempt from the GPO even though they're in the OU

---

## 5.2 Restricted Groups

**Purpose:** Control group membership via GPO — membership can ONLY be changed through the GPO settings, not through ADUC.

**Key behavior:** If you create a Restricted Group in a GPO and add members, any membership changes made via ADUC are **overridden** when the GPO processes.

---

## 5.3 Advanced Audit Policy

**Purpose:** More granular auditing than basic audit policy.

**Example — Track logon failures and account lockout:**
1. Create GPO → navigate to `Computer Configuration\Policies\Windows Settings\Security Settings\Advanced Audit Policy Configuration\Audit Policy Configuration\Logon/Logoff`
2. Enable "Audit Logon" → Failure
3. Enable "Audit Account Lockout" → Failure
4. Set Account Lockout Threshold (e.g., 3 failures)
5. **Important:** GPO must be link order 1 to work with Default Domain Policy
6. Review in Event Viewer → Windows Logs → Security → look for "Audit Failure"

---

## 5.4 RODC Pre-staging and Creation

1. On DC1 → ADUC → Domain Controllers OU → "Pre-create Read-only Domain Controller account"
2. Set hostname (e.g., "rodc"), complete wizard
3. On RODC VM: Install AD DS role → Promote → join existing domain → it auto-detects pre-staged account
4. Verify in ADUC → Domain Controllers OU shows RODC with read-only indicator
5. Connecting ADUC to RODC: no write operations available

---

## 5.5 AD Backup and Restore Process

**Backup:**
1. Windows Server Backup → Local Backup → Backup Once → Custom → System State → VSS Full Backup → destination

**Simulate failure:** Delete an OU (after unchecking accidental deletion protection)

**Restore via DSRM:**
1. `bcdedit /set safeboot dsrepair` → reboot
2. Login as `.\Administrator` (not domain admin — AD is offline)
3. `wbadmin get versions -backuptarget:E: -machine:dc1`
4. `wbadmin start systemstaterecovery -version:<identifier> -backuptarget:E: -machine:dc1`
5. Reboot

**Mark as authoritative:**
```
ntdsutil
activate instance ntds
authoritative restore
restore subtree "ou=TechSupport,ou=ITAdministrators,dc=example,dc=com"
quit
quit
```
6. `bcdedit /deletevalue safeboot` → reboot

---

## 5.6 AD Snapshots

**Create:**
```
ntdsutil
activate instance ntds
snapshot
create
list all
```

**Mount and view:**
```
mount <GUID>
quit
quit
dsamain -dbpath '<MountPoint>\windows\ntds\ntds.dit' -ldapport 5000
```
Then in ADUC → Change Domain Controller → `DC1:5000`

**Limitation:** Can only view/read — **cannot restore** from snapshots.

**Unmount:**
```
ntdsutil
activate instance ntds
snapshot
list all
unmount <GUID>
quit
quit
```

---

# Quick Reference: Key Differences to Remember

| Concept A | Concept B | Key Difference |
|-----------|-----------|----------------|
| Container | OU | OUs can link to GPOs, containers cannot |
| Default Domain Policy | Default Domain Controller Policy | DDP = all objects; DDCP = DCs only |
| Distribution group | Security group | Distribution = email only, no SID; Security = SID, permissions |
| Local GPO | Domain GPO | Local = single computer; Domain = all domain-joined |
| DAC | MAC | DAC = owner decides; MAC = security admin decides |
| Enforcing | Permissive | Enforcing = block + log; Permissive = log only, allow |
| `required` | `requisite` | Required = continues then denies; Requisite = immediate denial |
| Non-authoritative restore | Authoritative restore | Non-auth = DC updates from peers; Auth = DC pushes marked objects to peers |
| AD Snapshot | AD Backup | Snapshot = view only, cannot restore; Backup = can restore |
| Tombstone | Recycle Bin | Tombstone = auto after delete, 180 days; Recycle Bin = must enable, easier recovery |

---

# Exam Strategy for 5 Structured + 1 Long Question (40 min)

1. **Read all questions first** (1 min)
2. **Structured questions** (~5 min each = 25 min) — be concise, use bullet points, define terms clearly
3. **Long question** (~12 min) — this will likely combine multiple topics (e.g., GPO processing + inheritance + troubleshooting, or AD backup/restore + DSRM)
4. **Review** (2 min) — check you haven't missed sub-parts

**For every answer:**
- Define the term first
- Explain how it works
- Give an example or context from the practicals
- Use proper terminology from the slides (the professor uses specific terms)

---

*Good luck! You've got this. 🎯*
