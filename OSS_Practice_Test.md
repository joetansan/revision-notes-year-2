# IT2515 Operating System & Security — Practice Test
## Weeks 7–13 | 5 Structured Questions + 1 Long Question | 40 Minutes

> **Instructions:** Attempt all questions. Read each question carefully. For MCQs, choose the BEST answer. For short-answer questions, be concise but complete.

---

# SECTION A: Structured Questions (5 Questions)

---

## Question 1 — Directory Services & AD Structure

**(a)** Define the term "directory service" and state TWO key properties of a directory service's information store. **(3 marks)**

**(b)** Explain the difference between an AD **Domain**, a **Tree**, and a **Forest**. Include the relationship between them. **(6 marks)**

**(c)** State the THREE Active Directory database partitions and describe what each one contains and how far its replication extends. **(6 marks)**

<details>
<summary>🔑 Click to reveal answers for Question 1</summary>

**(a)**
- A directory service is a centralized database that maps network resources (users, printers, folders, devices) to their network addresses.
- Key properties (any two):
  - The backend database can be stored on different machines (distributed)
  - The database is not designed for transactional data (cannot handle high volume edits — but this is fine as directory data is stable)
  - It is often referred to as an "information store"
  - Can accommodate new object types and attributes (extensible)
  - Users and administrators can search for information from various locations
  - Accessible from many different operating systems (via LDAP)

**(b)**
- **Domain:** Logical grouping of network objects that share the same AD database. It is the basic building block of AD.
- **Tree:** Collection of one or more domains within a single contiguous namespace, linked together with transitive trust hierarchy. Example: example.com → sales.example.com
- **Forest:** Collection of one or more trees. Trees in a forest share a common global catalog, directory schema, logical structure, and directory configuration. The forest represents the security boundary of all accessible objects.
- **Relationship:** Forest contains Trees, Trees contain Domains.

**(c)**
| Partition | Contents | Replication |
|-----------|----------|-------------|
| Schema | Object and attribute definitions of the forest | All DCs within the forest |
| Configuration | Physical structure and configuration of the forest (sites, subnets, services) | All DCs within the forest |
| Domain | All domain objects (GPOs, users, groups, computers) | Only DCs of the same domain |

</details>

---

## Question 2 — AD Objects, Groups & Workgroups

**(a)** What is the difference between a **Security group** and a **Distribution group** in Active Directory? **(3 marks)**

**(b)** List and describe the FOUR available scopes of an Active Directory security group. **(4 marks)**

**(c)** Explain what the Security Account Manager (SAM) is, and describe what happens to the administrator credentials stored in SAM when a Windows Server is promoted to a Domain Controller. **(4 marks)**

**(d)** State TWO differences between a Windows **Workgroup** and an AD **Domain**. **(4 marks)**

<details>
<summary>🔑 Click to reveal answers for Question 2</summary>

**(a)**
- **Distribution group:** Used only with email applications. Has no Security Identifier (SID). Cannot be given permissions.
- **Security group:** A security principal with a SID. Can be given permissions. Can also be email-enabled. The default group type for any newly created group is Security.

**(b)**
| Scope | Description |
|-------|-------------|
| Local | Members can be assigned access permissions to local computer resources only |
| Domain Local | Members can access local domain resources only |
| Global | Members can access resources within the forest |
| Universal | Members can access resources within the forest |

**(c)**
- The SAM is a local database that holds all local user and group accounts. It authenticates all local user logins. It resides in `C:\Windows\System32\config`. Password hashes are stored in `HKEY_LOCAL_MACHINE\SAM`.
- Before promotion to a domain controller, local 'administrator' credentials are stored in the SAM. These are used for Directory Services Restore Mode (DSRM).
- After promotion to a domain controller, the administrator credentials move to the Active Directory database. The SAM credentials remain available only for DSRM login.

**(d)** Any two of:
- Workgroup = peer-to-peer, no central authentication; Domain = client-server with central authentication via Domain Controller
- Workgroup = each computer acts as both client and server; Domain = DC handles server role
- Workgroup = remote resource access requires account setup on each node; Domain = centralized permissions
- Workgroup = passwords cannot sync automatically; Domain = passwords synced via AD
- Workgroup = recommended for ≤15 computers; Domain = for enterprise environments

</details>

---

## Question 3 — Group Policy Objects (GPOs)

**(a)** Describe the TWO general types of Group Policy Objects. **(2 marks)**

**(b)** State the GPO processing order from lowest to highest precedence. When there are multiple GPOs at the same level, which one takes precedence? **(3 marks)**

**(c)** Explain the difference between GPO **Inheritance Blocking** and GPO **Enforcement**. Which one overrides the other? **(5 marks)**

**(d)** What is the purpose of **Resultant Set of Policies (RSoP)**? Name TWO ways to access it. **(3 marks)**

<details>
<summary>🔑 Click to reveal answers for Question 3</summary>

**(a)**
1. **Local GPOs** — Applicable only to the local computer. Managed via `gpedit.msc` or MMC with Group Policy Editor snap-in.
2. **Domain GPOs (Active Directory GPOs)** — Applicable to all domain-joined computers and user accounts. Managed via Group Policy Management tool on the DC.

**(b)**
- Processing order (lowest to highest precedence): **Local → Site → Domain → Organizational Unit**
- When multiple GPOs exist at the same level, they are processed by **reversed link order** — the GPO with link order number **1** has the highest precedence.
- For sub-OUs, GPOs linked to the OU closest to the user/computer object are processed last and have the highest precedence.

**(c)**
- **Inheritance Blocking:** A child OU can block inheritance from parent containers (domain, site, parent OU). This prevents parent GPOs from being applied to the child OU.
- **Enforcement:** A parent GPO can be enforced, meaning its settings take precedence over child object settings, even if the child OU has blocked inheritance.
- **Enforcement overrides Block Inheritance.** An enforced parent GPO will still apply even to a child OU that has blocked inheritance.

**(d)**
- RSoP is a report on all settings after GPOs have been processed. It is used for troubleshooting GPO implementations.
- Two ways to access:
  1. `rsop` command from the command line (must be admin account)
  2. RSoP snap-in via MMC (more flexible — can simulate processing on any container/user/computer)
- Also: `gpresult /v` for a text-based report

</details>

---

## Question 4 — Securing AD & Linux Security (SELinux)

**(a)** Name THREE security risks that motivate securing Active Directory Domain Services. **(3 marks)**

**(b)** Explain what a Read-Only Domain Controller (RODC) is and describe TWO scenarios where it would be used. **(4 marks)**

**(c)** Draw the Mandatory Access Control (MAC) evaluation flowchart. In your diagram, show the decision points for both DAC and MAC checks. **(4 marks)**

**(d)** Describe the THREE SELinux operating modes and explain when each would be used. **(4 marks)**

<details>
<summary>🔑 Click to reveal answers for Question 4</summary>

**(a)** Any three of:
- Network security threats
- Authentication attacks
- Elevation of privileges
- DoS attacks
- OS/system/service/application attacks
- Operational risks
- Physical security threats

**(b)**
- An RODC is a domain controller that contains AD data in **read-only mode** — it cannot edit AD data. All authentication requests are forwarded to normal (writable) DCs. It can optionally cache credentials for configured users.
- Scenarios:
  1. **Remote office sites** where secured facilities are challenging — if the RODC is compromised or stolen, security information is not exposed (except cached credentials)
  2. **Environments requiring reduced attack surface** — RODC contains all AD objects except security-related ones by default, limiting exposure of sensitive authentication data

**(c)**
```
Start
  ↓
Is DAC allowed on resource by the process?
  ├─ No  → Access Denied
  └─ Yes → Is MAC allowed on resource by the process?
              ├─ No  → Access Denied
              └─ Yes → Access Allowed
```
- DAC is evaluated first
- If DAC denies, MAC is not evaluated
- If DAC allows, MAC is then checked
- Both must allow for access to be granted

**(d)**
| Mode | Description | When Used |
|------|-------------|-----------|
| **Enforcing** (Default for CentOS) | SELinux policy is active. Access violations are logged AND disallowed. | Production environments — provides full MAC protection |
| **Permissive** | SELinux policy is active. Access violations are logged but ALLOWED. | Testing new applications under SELinux constraints — allows you to see what would be blocked without actually blocking |
| **Disabled** | SELinux policy is inactive. Access control defaults to DAC only. | When SELinux is not needed (not recommended for security-sensitive systems) |

</details>

---

## Question 5 — PAM & AD Account Security

**(a)** Explain what Pluggable Authentication Module (PAM) is and why it was introduced. What problem did it solve? **(3 marks)**

**(b)** Describe the FOUR types of PAM module interfaces. Is it necessary for a PAM configuration file to define all four? **(5 marks)**

**(c)** Explain the difference between the PAM control flags **required** and **requisite**. **(3 marks)**

**(d)** Describe THREE password policy settings that can be configured in Windows AD Account Security. **(3 marks)**

<details>
<summary>🔑 Click to reveal answers for Question 5</summary>

**(a)**
- PAM is an API framework for authentication-related services in Linux.
- Before PAM, every Linux application needing authentication had to develop its own system and associated database. This led to a complex system where each application/server had to be managed differently, and it was impossible to integrate OS password authentication into 3rd-party applications.
- PAM solved this by providing a common, pluggable authentication scheme — administrators and developers can add new authentication methods by installing PAM modules and modifying PAM configuration files.

**(b)**
| Interface | Purpose |
|-----------|---------|
| **auth** | Determines whether the user is who they claim to be (usually by password, biometrics, etc.) |
| **account** | Determines whether the user is allowed to access the service (password expired, account status, etc.) |
| **password** | Used for changing user passwords |
| **session** | Actions before/after authentication (mounting home directory, logging login/logout, restricting services) |

- **No**, it is not necessary for a PAM configuration file to define all four interfaces.

**(c)**
- **required:** Module failure results in interface failure, but PAM still calls all remaining modules listed for this interface before denying authentication. The failure is noted but processing continues.
- **requisite:** Module failure results in **immediate** denial of authentication. Processing stops right away.

**(d)** Any three of:
| Setting | Description |
|---------|-------------|
| **Enforce password history** | Defines how many previous passwords a user cannot reuse |
| **Maximum password age** | Maximum time before the next required password change |
| **Minimum password age** | Minimum time before password can be changed (must be less than max) |
| **Minimum password length** | Minimum number of characters required |
| **Password complexity requirements** | Cannot contain username; ≥6 chars; must contain characters from 3 of 4 groups (uppercase, lowercase, numeric, special) |

</details>

---

# SECTION B: Long Question (1 Question)

---

## Question 6 — AD Backup, Restore & GPO Troubleshooting

A company has an Active Directory domain with two Domain Controllers (DC1 and DC2). The IT administrator accidentally deleted the "Finance" OU on DC1. The AD Recycle Bin was NOT enabled.

**(a)** Explain what happens to the deleted "Finance" OU object in Active Directory. What is a tombstone object, and what is its default lifespan? **(4 marks)**

**(b)** Since the AD Recycle Bin is not available, describe the complete step-by-step process to restore the deleted "Finance" OU using a backup. Include:
- How to enter Directory Services Restore Mode (DSRM)
- How to perform the system state restoration
- How to mark the restoration as authoritative
- How to exit DSRM and resume normal operation **(10 marks)**

**(c)** The administrator also created a GPO called "Restrict Finance Access" linked to the Finance OU before it was deleted. After restoring the OU, the GPO settings are not applying to users in the Finance OU. Explain how the administrator can use **RSoP** and **gpresult** to troubleshoot this issue, and describe what the administrator should check regarding GPO link order and inheritance. **(6 marks)**

<details>
<summary>🔑 Click to reveal answers for Question 6</summary>

**(a)**
- When the "Finance" OU is deleted, it becomes a **tombstone object**. It is moved into a special container called "Deleted Objects".
- A tombstone is a remnant of a deleted AD object that ensures:
  1. Correct replication of the delete action across peer domain controllers
  2. Correct object deletion state after AD restore (if restored from backup before the delete, the tombstone ensures it remains deleted)
- **Default lifespan:** 180 days, after which the tombstone is fully and permanently removed.

**(b) Complete AD Restore Process:**

**Step 1: Enter DSRM**
- On DC1, open PowerShell and run:
  - `bcdedit /set safeboot dsrepair`
  - `shutdown –t 0 /r`
- Alternatively, press F8 on OS load screen
- DC1 will restart in DSRM mode (AD is offline)

**Step 2: Login**
- Login as `.\Administrator` (local admin) — cannot login as domain administrator since AD is offline

**Step 3: Check available backups**
- Open PowerShell and run:
  - `wbadmin get versions -backuptarget:E: -machine:dc1`
- Note the version identifier returned

**Step 4: Perform system state restoration**
- Run: `wbadmin start systemstaterecovery -version:<version_identifier> -backuptarget:E: -machine:dc1`
- Type 'y' twice to confirm
- Wait for restoration to complete (~30 minutes)
- When prompted to restart, type 'y'

**Step 5: Mark restoration as authoritative**
- After reboot, login as `.\Administrator` again (still in DSRM)
- Open PowerShell and run the following commands:
  - `ntdsutil`
  - `activate instance ntds`
  - `authoritative restore`
  - `restore subtree "ou=Finance,dc=example,dc=com"` (adjust DN as needed)
- Click 'Yes' in the pop-up to confirm
- Type `quit` twice to exit ntdsutil

**Step 6: Exit DSRM and resume normal operation**
- Run: `bcdedit /deletevalue safeboot`
- Reboot DC1
- DC1 will now start normally with AD DS running
- Verify the "Finance" OU exists using Active Directory Users and Computers
- DC1 will push the authoritative "Finance" OU data to DC2

**(c) Troubleshooting with RSoP and gpresult:**

**Using RSoP:**
1. On a client machine, login as a Finance OU user
2. Open PowerShell and run `rsop.msc`
3. The RSoP GUI will show all applied GPO settings
4. Navigate to the relevant configuration section to check if "Restrict Finance Access" settings appear
5. If settings don't appear, the GPO is not being applied

**Using gpresult:**
1. On the client machine, run `gpresult /v` in PowerShell
2. This generates a text-based report showing all applied GPOs
3. Check if "Restrict Finance Access" is listed among the applied GPOs

**What to check:**
1. **GPO Link:** Verify the GPO is actually linked to the restored Finance OU (the link may have been lost during deletion/restoration — the GPO itself may still exist in the "Group Policy Objects" container but needs to be re-linked)
2. **Link Order:** If multiple GPOs are linked to the Finance OU, check the link order. The GPO with link order number 1 has the highest precedence. Conflicting settings from a higher-precedence GPO may override "Restrict Finance Access"
3. **Inheritance:** Check if the Finance OU has inherited conflicting GPOs from parent containers (domain, site). A parent GPO with different settings may override the Finance OU GPO
4. **Enforcement:** Check if any parent GPO is enforced — enforced GPOs take precedence even over closer GPOs
5. **Block Inheritance:** Check if Block Inheritance is enabled on the Finance OU, which would block parent GPOs but may also affect the expected processing order
6. **GPO Status:** Verify the GPO is enabled (not disabled) and the specific settings within it are configured correctly

</details>

---

# Answer Key Summary

| Question | Topic | Key Points |
|----------|-------|------------|
| Q1 | Directory Services & AD Structure | Directory service definition, Domains/Trees/Forests, 3 AD partitions |
| Q2 | AD Objects, Groups & Workgroups | Security vs Distribution groups, Group scopes, SAM, Workgroup vs Domain |
| Q3 | GPOs | Types, Processing order, Inheritance/Enforcement, RSoP |
| Q4 | Securing AD & SELinux | Risks, RODC, MAC flowchart, SELinux modes |
| Q5 | PAM & Account Security | PAM purpose, 4 interfaces, Control flags, Password policies |
| Q6 | AD Backup/Restore & GPO Troubleshooting | Tombstones, DSRM restore process, Authoritative restore, RSoP troubleshooting |

---

*Time yourself: 40 minutes total. Good luck! 🎯*
