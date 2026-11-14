# IT2515 Operating System & Security — Test (Based on Recall)
## Weeks 7–13 | Total: 20 Marks

> **Instructions:** Answer all questions. Each question is **2 marks** unless otherwise stated.

---

## Question 1 (2 marks)
**Define Pluggable Authentication Module (PAM).**

<details>
<summary>🔑 Click to reveal answer</summary>

**PAM (Pluggable Authentication Module)** is an **API framework** for authentication-related services on Linux systems.

**Motivation (1 mark):**
Before PAM, every Linux application that needed authentication features had to develop its own authentication system and associated database. This led to a complex system where each application/server had to be managed and administered differently. It was also impossible to integrate OS password authentication into 3rd-party applications. PAM was introduced to solve this by providing a **common, pluggable authentication scheme** that can be used across a wide variety of applications.

**What PAM contains (1 mark):**
PAM provides a single, fully-documented library with **four module interfaces**:
1. **auth** — Determines whether the user is who they claim to be (e.g., password, biometrics)
2. **account** — Determines whether the user is allowed to access the service (e.g., password expired, account status)
3. **password** — Used for changing user passwords
4. **session** — Actions performed before/after authentication (e.g., mounting home directory, logging, resource restrictions)

> Not all four interfaces need to be defined in every PAM configuration file.

</details>

---

## Question 2 (2 marks)
**What is contained inside a SELinux Security Policy?**

<details>
<summary>🔑 Click to reveal answer</summary>

A SELinux Security Policy contains:

1. **Access rules** (1 mark) — Rules that define what actions subjects (processes/users) are allowed to perform on objects (files/resources). Example: `allow system_t bin_t:file execute;`

2. **Default security contexts** (1 mark) — Pre-defined security context labels (`SELinux_user:role:type:level`) for any process, file, or login user on the system.

> Most Linux distributions adapt from a **reference policy** (https://github.com/SELinuxProject/refpolicy).

</details>

---

## Question 3 (10 marks)
**PAM Configuration File Evaluation**

The following is the PAM configuration file for the SSHD service located at `/etc/pam.d/sshd`:

```
#%PAM-1.0
auth    [ignore=ignore success=done]  pam_succeed_if.so uid >= 1000
auth    [ignore=ignore success=done]  pam_succeed_if.so user ingroup users
auth    sufficient                     pam_unix.so
auth    sufficient                     pam_permit.so
```

**Scenario:** A non-local user with UID **999** attempts to log in via SSH. This user does NOT exist in the local `/etc/passwd` file. The user is also NOT a member of the `users` group.

For **each** of the four `auth` module lines, state:
1. Whether the module **succeeds or fails**
2. The **result** returned by the control flag (e.g., ok, done, ignore)

Then state the **overall auth result** for this login attempt — is authentication **allowed or denied**?

| Module | Result (Succeed/Fail) | Control Flag Result | (2 marks each) |
|--------|----------------------|---------------------|----------------|
| Line 1: `pam_succeed_if.so uid >= 1000` | | | |
| Line 2: `pam_succeed_if.so user ingroup users` | | | |
| Line 3: `pam_unix.so` | | | |
| Line 4: `pam_permit.so` | | | |

**Overall authentication result:** (2 marks)

<details>
<summary>🔑 Click to reveal answer</summary>

**Understanding the control syntax:**
- `[ignore=ignore success=done]` — `ignore=ignore` means if the module **fails**, the result is **ignored** (does not affect the overall result). `success=done` means if the module **succeeds**, processing **stops immediately** and the result is "done" (overall success).

**The user:** Non-local user, UID = 999, not in `/etc/passwd`, not in `users` group

### Line-by-line evaluation:

| Line | Module | Succeed/Fail? | Control Result | Explanation |
|------|--------|--------------|----------------|-------------|
| **Line 1** | `pam_succeed_if.so uid >= 1000` | **Fail** | **Ignore** (result discarded, processing continues) | UID is 999, which is NOT >= 1000. The check fails. Under `ignore=ignore`, this failure is **ignored** — it does not affect the overall result and processing moves to the next module. |
| **Line 2** | `pam_succeed_if.so user ingroup users` | **Fail** | **Ignore** (result discarded, processing continues) | The user is NOT a member of the `users` group. The check fails. Under `ignore=ignore`, this failure is also **ignored** — processing continues. |
| **Line 3** | `pam_unix.so` | **Fail** | **Ignored** (failure of sufficient module, processing continues) | This user is non-local and does NOT exist in `/etc/passwd`. The local password check **fails**. Under `sufficient`, a failure is **ignored** — processing continues to the next module. |
| **Line 4** | `pam_permit.so` | **Succeed** | **Done** (success, processing stops) | `pam_permit.so` always returns success (it unconditionally permits access). Under `sufficient`, and since no previous `required` modules have failed (none exist), the result is **done** — authentication succeeds. |

### Overall Authentication Result:

**Authentication is ALLOWED.**

**Reasoning:** The final module (`pam_permit.so`) with `sufficient` control flag succeeds. Since there are no `required` modules in this config, there are no prior failures to block the result. The `sufficient` success from Line 4 concludes the auth interface as **success**. The non-local user with UID 999 is authenticated.

</details>

---

## Question 4 (2 marks)
**Define Authoritative Restore of Active Directory.**

<details>
<summary>🔑 Click to reveal answer</summary>

**Authoritative Restore** is a method of restoring an Active Directory Domain Server to a previously known state where **specific objects are marked as the authoritative (only good) copies** (1 mark).

- After restoration, the DC sends the authoritative object updates to all peer DCs.
- The DC receives updates from peer DCs about non-authoritative objects.

**Difference from Non-Authoritative Restore** (1 mark):
- **Non-Authoritative (Normal) Restore:** Restores DC to a previously known state, then the DC **updates from peer DCs** (the restored DC gets the latest data from partners).
- **Authoritative Restore:** Restores DC and **marks specific objects as authoritative** — these objects are pushed TO peer DCs, overwriting their copies. Used when the restored data must be the definitive version (e.g., recovering a deleted OU when AD Recycle Bin is not available).

</details>

---

## Question 5 (2 marks)
**What is an AD Server Snapshot?** State the tool used to create and manage snapshots, and explain whether AD data can be restored from a snapshot.

<details>
<summary>🔑 Click to reveal answer</summary>

An **AD Server Snapshot** is an **exact copy of a historical state** of Active Directory Domain Services at the time the snapshot was taken (1 mark).

- **Tool used:** `ntdsutil` — used to create, mount, list, and unmount AD snapshots.
- **Limitation:** AD data **cannot be restored from a snapshot**. Snapshots are **read-only** and can only be used for **viewing/examining** historical AD data (verifying AD state), not for restoration.

(1 mark for tool + limitation)

</details>

---

## Question 6 (2 marks)
**An administrator encounters issues after implementing SELinux on a production server. Applications are being blocked by SELinux policy violations, but the administrator needs to identify exactly which access is being denied without compromising security.**

<details>
<summary>🔑 Click to reveal answer</summary>

The administrator should switch to **Permissive** mode. (1 mark)

**Why:** In Permissive mode, SELinux security policy remains **active** and any access violations are **logged** (recorded in audit logs), but access is **allowed** instead of blocked (1 mark). This allows the administrator to:
- Identify exactly which access is being denied by reviewing the logs
- Diagnose SELinux policy violations without breaking application functionality
- Use tools like the SELinux Troubleshooter (`setroubleshoot`) to analyze violations and determine the correct policy fixes
- After fixing the issues, switch back to Enforcing mode

> **Note:** Permissive mode is temporary if set via `setenforce 0` (resets on reboot). To persist, edit `/etc/selinux/config` and set `SELINUX=permissive`.

</details>

---

## Mark Summary

| Question | Topic | Marks |
|----------|-------|-------|
| Q1 | Define PAM | 2 |
| Q2 | SELinux Security Policy contents | 2 |
| Q3 | PAM Config Evaluation | 10 |
| Q4 | Authoritative Restore | 2 |
| Q5 | AD Snapshots | 2 |
| Q6 | SELinux Mode for troubleshooting | 2 |
| **Total** | | **20** |
