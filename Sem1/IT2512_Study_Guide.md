# IT2512 Practical Test — Study Guide

> **Read this the night before and the morning of your test.**
> Sections marked ⚠️ are your weak areas — spend extra time there.

---

## How the Test is Structured

| Section | Type | Questions | Marks |
|---------|------|-----------|-------|
| A | MCQ | 4 questions | 4 marks |
| B | Coding | 2 questions (14 + 18) | 32 marks |
| C | Short Answer | 3 questions (3 × 8) | 24 marks |

- You can write Python/Flask, Python/Flask-like code, or pseudocode embedded in copied code
- Colour changed/added lines in **BLUE**
- Syntax errors are NOT penalised unless they change the intended logic
- Show parameterised queries with `?` placeholders — don't just write "use a parameterised query"
- You can assume `get_current_user()`, `get_record()`, `get_user()` helpers exist

---

## Topic 2.1 — Introduction to Secure Coding

### The Core Mindset Shift

```
FROM  "Does it work?"
TO    "Can it be misused?"
TO    "What should the server enforce?"
```

A feature can work perfectly for normal use and still be **insecure**. Secure coding is not about stopping hackers — it's about not making unsafe assumptions.

### The Four Ideas

| Idea | What It Means | StaffHub Example |
|------|---------------|------------------|
| **Secure coding mindset** | Don't assume a request is safe just because it came from the app's own UI | An employee changing the record ID in the URL from `/records/view/1048` to `/records/view/1049` |
| **Trust boundary** | Point where data crosses from less trusted to more trusted area (browser → server) | Data from the browser should be treated as untrusted until the server checks it |
| **Server-side responsibility** | The server enforces security, not the browser | Dropdown only shows "Low/Medium/High" but server must still reject "Deleted" |
| **Secure defaults** | Start from the safer behaviour | If access is unclear → deny. If input is invalid → reject. If error occurs → show safe message. |

### What is Untrusted Input?

**Everything from the browser is untrusted:**
- Form fields (including hidden fields!)
- URL parameters
- Dropdown selections
- Cookies and headers
- Uploaded files

**NOT untrusted:**
- Server-side configuration values
- Values read from your own database (after you put them there safely)

### 🔑 The One Rule That Covers Most Questions

> **Client-side checks (dropdowns, hidden buttons, maxlength, JavaScript) are for usability. Server-side checks are for security. Never rely on client-side controls alone.**

---

## Topic 2.2 — Secure Coding Fundamentals

### Control 1: Input Validation

**What:** Check whether incoming data is acceptable **before** the application uses it.

**What to check:**
- **Type** — is it a string, integer, etc.?
- **Length** — is it within the allowed range? (e.g. max 50 chars for search, max 500 for comments)
- **Format** — does it match the expected pattern?
- **Range** — is the value within bounds?
- **Allowed values** — is it one of the expected values?

**Allowlist vs Blocklist:**

| Approach | How It Works | When to Use |
|----------|-------------|-------------|
| **Allowlist** ✅ | Accept ONLY values that match a known-good list | Predictable fields (priority, category, role, status, decision) |
| **Blocklist** ❌ | Reject values that match a known-bad list | Unreliable — attackers can bypass by finding values not on the list |

**Always prefer allowlist validation for predictable StaffHub fields:**

```python
# Category — allowlist
if category not in {"IT Support", "HR", "Facilities", "Finance", "General"}:
    abort(400)

# Priority — allowlist
if priority not in {"Low", "Medium", "High"}:
    abort(400)

# Decision — allowlist
if decision not in {"Approved", "Rejected"}:
    abort(400)
```

**For free-text fields (search, description), validate length and characters:**

```python
import re

q = request.args.get("q", "").strip()

# Length check
if len(q) > 50:
    return error("Search text must be 50 characters or fewer."), 400

# Character allowlist
if q and not re.fullmatch(r"[A-Za-z0-9 _-]+", q):
    return error("Search text contains unsupported characters."), 400
```

### Control 2: Parameterised Queries

**What:** Separate the SQL instruction from user-provided values using `?` placeholders.

**UNSAFE (string concatenation / f-string):**
```python
# ❌ User input is part of the SQL command
sql = f"SELECT * FROM records WHERE title LIKE '%{q}%'"
db.execute(sql)
```

**SAFE (parameterised):**
```python
# ✅ User input is passed as data, not part of the SQL command
db.execute(
    "SELECT * FROM records WHERE title LIKE ?",
    (f"%{q}%",)
)
```

**The key difference:** In the unsafe version, if `q = "' OR '1'='1"`, it becomes part of the SQL command. In the safe version, the database treats `q` as a literal string value, not as SQL.

**Common mistake:** Writing "use a parameterised query" without showing the query structure. You MUST show the `?` placeholders and the tuple of values.

### Control 3: Output Encoding

**What:** When displaying user-submitted data in HTML, encode it so the browser treats it as text, not as HTML/JavaScript.

**Why:** If an employee submits `<script>alert('hacked')</script>` as a description, and the page renders it as raw HTML, the script executes for every user who views that record.

**In Jinja2 templates:**
- `{{ variable }}` — auto-escapes by default (safe ✅)
- `{{ variable | safe }}` — renders raw HTML (UNSAFE ❌ for user content)
- Never mark user-submitted content as `| safe`

### Control 4: Safer Error Handling

**UNSAFE:**
```python
except Exception as e:
    return f"Database error: {e}", 500    # ❌ Shows SQL errors, table names, etc.
```

**SAFE:**
```python
except Exception:
    app.logger.exception("Record search failed")     # Log technical details on server
    return render_template("error.html",
        error="Search is temporarily unavailable."), 500  # Show friendly message to user
```

**The rule:** Technical error details go in the **server log**. Users see a **controlled message**.

### ⚠️ Validation vs Output Encoding — Know the Difference!

| | Validation | Output Encoding |
|---|-----------|----------------|
| **When** | Before the application uses the data | When displaying data in a page |
| **Purpose** | Is this data acceptable? | Display this data safely in HTML |
| **Example** | Reject priority "Deleted" because it's not in the allowlist | Encode `<script>` as `&lt;script&gt;` so it displays as text |
| **They are NOT the same thing** | Rejects bad input | Makes any input safe to display |

Both are needed. Validation rejects bad input. Output encoding protects against anything that slipped through.

### ⚠️ The Search Route Pattern (Lab 2.1/2.2 — This Will Be Tested!)

The secure search route follows this order:

```
1. Get input    →  q = request.args.get("q", "").strip()
2. Validate     →  Check length (max 50), check characters (regex)
3. Query        →  Use parameterised query with ? placeholders
4. Error handle →  try/except, log on server, show friendly message
5. Return       →  render_template with results
```

---

## Topic 2.3 — Advanced Secure Coding (Refactoring)

### ⚠️ The Approval Route Pattern (This Will Be Tested!)

This is the pattern that cost you the most marks. Memorise this flow:

```python
@app.route("/records/<int:record_id>/decision", methods=["POST"])
def decide_record(record_id):

    # STEP 1: Identify current user from session + database
    user = get_current_user()
    if user is None:
        abort(401)                          # Not logged in

    # STEP 2: Validate submitted decision
    decision = request.form.get("decision", "")
    if decision not in {"Approved", "Rejected"}:
        abort(400)                          # Invalid value

    # STEP 3: Validate comment length
    comment = request.form.get("comment", "").strip()
    if len(comment) > 500:
        abort(400)                          # Too long

    # STEP 4: Load the current record
    record = get_record(record_id)
    if record is None:
        abort(404)                          # Record doesn't exist

    # STEP 5: Check authorisation
    if not can_review_record(user, record):
        abort(403)                          # Not allowed

    # STEP 6: Update only if still Pending
    cursor = get_db().execute(
        """
        UPDATE records
        SET status = ?,
            reviewed_by = ?,
            manager_comment = ?,
            updated_at = CURRENT_TIMESTAMP
        WHERE id = ? AND status = 'Pending'
        """,
        (decision, user["id"], comment, record_id)
    )
    get_db().commit()

    if cursor.rowcount != 1:
        abort(409)                          # Record changed state

    return redirect("/records")
```

### ⚠️ The `get_current_user()` Pattern — Your Biggest Weakness

**What you were doing (wrong):**
```python
session = get_current_user()     # Called it, but...
# ...later in the code:
if role != "Manager":            # ❌ `role` is UNDEFINED
(decision, user_id, ...)         # ❌ `user_id` is UNDEFINED
```

**What you need to do (correct):**
```python
user = get_current_user()        # Store the returned user object
if user is None:                 # Check if logged in
    abort(401)

# Now use the user object's fields:
user["id"]         # e.g. 3
user["role"]       # e.g. "Manager"
user["department"] # e.g. "HR"
user["username"]   # e.g. "ben"
```

**The helper returns a dictionary, not magic variables.** You must access fields using `user["role"]`, not bare `role`.

### The Two Helpers

**`get_current_user()` — WHO is logged in?**
```python
def get_current_user():
    user_id = session.get("user_id")    # Read from server-side session
    if user_id is None:
        return None
    return get_db().execute(
        "SELECT id, username, role, department FROM users WHERE id = ?",
        (user_id,)
    ).fetchone()
```
- Reads user ID from **server-side session** (not from form fields!)
- Loads role and department from the **database**
- Returns a dict or None

**`can_review_record(user, record)` — Is this user ALLOWED to review this record?**
```python
def can_review_record(user, record):
    if user["role"] == "Admin":
        return True
    if user["role"] == "Manager" and user["department"] == record["department"]:
        return True
    return False
```
- Admins → can review anything
- Managers → can review their own department only
- Employees → cannot review anything

### The StaffHub Review Rules (Memorise These)

| Role | Can Do | Cannot Do |
|------|--------|-----------|
| Employee | Submit records, view own records | Cannot approve/reject any record |
| Manager | Approve/reject records from own department | Cannot approve other departments |
| Admin | Approve/reject any record | — |
| Any role | — | Cannot review records that are not Pending |

### Hidden Fields Are NOT Security Data

The original route trusted `request.form["role"]` and `request.form["department"]`. These came from hidden HTML fields:

```html
<input type="hidden" name="role" value="Manager">
<input type="hidden" name="department" value="HR">
```

**Why this is dangerous:** Anyone can change hidden fields using browser Developer Tools (right-click → Inspect → edit the HTML). An Employee could change `value="Employee"` to `value="Manager"` and bypass the role check.

**The fix:** Never read security-critical values (user_id, role, department, permission) from form fields. Always load them from the server-side session and database using `get_current_user()`.

### Race Conditions / Stale State

**What it is:** Between the time you read a record's status and the time you update it, another request might have already changed it.

**Example:** Two managers approve the same record at the same time. Both read `status = "Pending"`. Both update. The record gets approved twice.

**The fix:** Include the status check in the UPDATE WHERE clause:
```sql
UPDATE records SET status = ? WHERE id = ? AND status = 'Pending'
```
Then check `cursor.rowcount` — if it's 0, the record was already changed.

### ⚠️ The `| safe` Trap (Optional Challenge from Lab 2.3)

```html
<p>{{ record.manager_comment | safe }}</p>    <!-- ❌ UNSAFE -->
<p>{{ record.manager_comment }}</p>            <!-- ✅ SAFE -->
```

The `| safe` filter tells Jinja2 to render the content as raw HTML. If `manager_comment` contains `<script>alert('x')</script>`, it will execute. Without `| safe`, Jinja2 auto-escapes HTML entities.

**Rule:** Never use `| safe` on user-submitted content.

---

## Topic 2.4 — Secure SDLC & Code Review

### The Big Idea

> A feature is not secure just because it works. A feature is more trustworthy when the team can **show** the security requirement was clear, the design supported it, the review checked it, the tests verified it, and the release decision used evidence.

### Security Checkpoints Across the Lifecycle

| Checkpoint | Key Question | Evidence |
|------------|-------------|----------|
| **Requirement** | Is the security behaviour written clearly enough to test? | "Only authorised managers and admins may approve/reject records. Managers may only review records in their department." |
| **Design** | Has the team decided WHERE the rule will be enforced? | "The backend route must check logged-in user's role and record-level permission before updating status." |
| **Implementation** | Can a reviewer identify WHERE the security requirement is implemented? | Merge request identifies the route and helper function responsible for authorisation. |
| **Code Review** | Has another person checked the security-sensitive logic? | Reviewer asks: Who can call this route? What data is trusted? What happens if wrong role? What if record is out of scope? |
| **Verification** | Has the team tested BOTH allowed AND blocked cases? | Test log: "Employee approval attempt → Expected: 403 → Observed: 403" |
| **Release** | Is there enough evidence to release? | Checklist: requirement documented, review completed, negative tests passed, known issues recorded. |
| **Vulnerability Response** | If a bug escapes, how does the team fix AND improve? | Log the issue, fix root cause, verify fix, add regression test, update review checklist. |

### NIST SSDF — Four Practice Groups

| Group | Question It Answers | StaffHub Example |
|-------|--------------------|--------------------|
| **Prepare the Organisation** | "Do we know what secure work looks like before we start?" | Team agrees: any status-changing feature needs security requirement, design review, code review, and verification evidence. |
| **Protect the Software** | "Can we trust the code and release package?" | Only authorised team members can approve changes to the main branch. |
| **Produce Well-Secured Software** | "Did we build and check the feature properly before release?" | Manager approval workflow is reviewed and tested, especially for unauthorised access attempts. |
| **Respond to Vulnerabilities** | "When something goes wrong, do we fix the system AND the process?" | Missing authorisation check is logged, fixed, verified, and added to review checklist. |

### ⚠️ Code Review Questions vs Release Checklist Items

This distinction cost you 2 marks. Know the difference:

**Code review questions (about the code's security behaviour):**
1. Does the route check whether the user is logged in?
2. Does the route verify the user's role and permission before allowing the action?
3. What happens if an Employee sends the request directly to the endpoint?
4. Where is the authorisation rule enforced — server code or just the UI?
5. Does the route reject invalid input values?
6. Does the route handle records that are no longer in the expected state?

**Release checklist items (about process paperwork):**
1. Security requirement documented? ✅
2. Review checklist completed? ✅
3. Verification log includes blocked cases? ✅
4. Known issues recorded? ✅

**Both are important. But if the question asks "what should a code reviewer ask?" — give code review questions, not checklist items.**

### Defect Escape Analysis

When a security bug escapes to production, ask:

| Question | Example |
|----------|---------|
| What is the escaped issue? | Alice can edit Bob's record by changing the record_id |
| What is the security impact? | Unauthorised data modification |
| Which checkpoint should have caught it first? | Requirement (if vague) or Design (if ownership enforcement not planned) |
| Which later checkpoint could still have caught it? | Verification (if negative test cases were required) |
| What evidence was missing? | Test case: "Alice tries to edit Bob's record → Expected: rejected" |
| What process improvement? | Add ownership check requirement to review checklist for all edit routes |

### Strong vs Weak Requirements

| Weak | Strong |
|------|--------|
| "Managers can approve records" | "Only authenticated users with Manager or Admin role may approve or reject records, and managers may only review records within their authorised scope." |
| "Employees can edit records" | "The system shall allow authenticated employees to edit only records they own that are still Pending. The system shall reject attempts to edit another user's record or any record that has already been approved, rejected, or closed." |

A strong requirement states: **WHO** can act, **WHAT** they can do, and **WHAT must be blocked**.

### Verification Test Cases — The Template

For any StaffHub feature, write test cases covering:

| Category | Example |
|----------|---------|
| ✅ Successful case | Manager approves own department's pending record → Record becomes Approved |
| ❌ Unauthenticated | User not logged in attempts action → 401 |
| ❌ Wrong role | Employee attempts approval → 403 |
| ❌ Wrong scope | Manager approves another department's record → 403 |
| ❌ Wrong state | User approves already-approved record → 409 |
| ❌ Invalid input | User submits decision "Maybe" → 400 |

---

## ⚠️ Your Weaknesses — Specific Fixes

### Weakness 1: "SQL injection" as default risk answer

**The problem:** You wrote "SQL injection attack risk" when the code already had `?` parameterised queries.

**The rule:**
- Code uses `f"...{user_input}..."` in SQL → risk is **SQL injection** ✅
- Code uses `?` placeholders → risk is **NOT** SQL injection ❌

**When you see parameterised queries, the risks are:**
- **Authorisation bypass** — the query runs, but for the wrong user (untrusted data driving security decisions)
- **Data corruption** — invalid values written to database (no allowlist validation)
- **Stale state / race conditions** — record changed between read and update

### Weakness 2: Not unpacking `get_current_user()`

**Your pattern (wrong):**
```python
session = get_current_user()
# ...later:
if role != "Manager":       # NameError: 'role' is not defined
```

**Correct pattern (memorise this):**
```python
user = get_current_user()
if user is None:
    abort(401)
# Use user["role"], user["id"], user["department"] from here on
```

**Think of it like this:** `get_current_user()` gives you a box (a dictionary). You need to open the box and take out the items inside (`user["role"]`, `user["id"]`, etc.). You can't use `role` by itself — that variable doesn't exist.

### Weakness 3: Code review questions vs release checklist

**How to tell them apart:**
- If the question is about **what the code does** → code review question
- If the question is about **whether the process was followed** → release checklist item

**Quick test:** Can you answer the question by looking at the code? If yes, it's a code review question. If you need to look at paperwork/process documents, it's a checklist item.

### Weakness 4: Error handling

**Always mention error handling when asked about weaknesses in a route that has no try/except.** The pattern:

```python
try:
    records = db.execute("SELECT ... WHERE title LIKE ?", (f"%{q}%",)).fetchall()
except Exception:
    app.logger.exception("Search failed")
    return render_template("error.html", error="Search is temporarily unavailable."), 500
```

If the question asks "what could go wrong" with a route that has no error handling, the answer is: **raw database/Python error details (table names, SQL queries, stack traces) could be displayed to the user, leaking internal application information.**

### Weakness 5: Repeating the same finding

When asked for multiple findings, think about different **categories**:

| Category | Example Finding |
|----------|----------------|
| Authentication | Route doesn't check if user is logged in |
| Authorisation | Route doesn't check if user is allowed to perform this action |
| Input validation | Route doesn't validate title length, priority allowlist, etc. |
| State management | Route doesn't check if record is still Pending/Editable |
| Error handling | Route has no try/except, could leak error details |
| Query safety | Route uses string concatenation instead of parameterised queries |

Pick from different categories and you'll never repeat yourself.

---

## Quick Reference — HTTP Status Codes

| Code | Name | When to Use |
|------|------|-------------|
| 400 | Bad Request | Invalid input: wrong decision value, comment too long, bad characters |
| 401 | Unauthenticated | User is not logged in (`get_current_user()` returns None) |
| 403 | Forbidden | User is logged in but not allowed: wrong role, wrong department, not the owner |
| 404 | Not Found | Record or user doesn't exist |
| 409 | Conflict | Record state has changed (e.g. already approved, already rejected) |

---

## Quick Reference — Common StaffHub Fields and Validation

| Field | Validation Rule |
|-------|----------------|
| Search keyword | Max 50 chars, allow `[A-Za-z0-9 _-]+` |
| Title | Required, max 80 chars |
| Category | Allowlist: `{"IT Support", "HR", "Facilities", "Finance", "General"}` |
| Description | Max 1000 chars |
| Priority | Allowlist: `{"Low", "Medium", "High"}` |
| Decision | Allowlist: `{"Approved", "Rejected"}` |
| Manager comment | Max 500 chars |

---

## Quick Reference — Code Patterns to Copy-Paste in the Test

### Pattern: Validate and search
```python
q = request.args.get("q", "").strip()
if len(q) > 50:
    return render_template("search.html", records=[], q="", error="..."), 400
if q and not re.fullmatch(r"[A-Za-z0-9 _-]+", q):
    return render_template("search.html", records=[], q="", error="..."), 400
try:
    records = db.execute(
        "SELECT id, title, description, status FROM records WHERE title LIKE ?",
        (f"%{q}%",)
    ).fetchall()
except Exception:
    app.logger.exception("Record search failed")
    return render_template("search.html", records=[], q="", error="..."), 500
```

### Pattern: Identify user and authorise
```python
user = get_current_user()
if user is None:
    abort(401)
record = get_record(record_id)
if record is None:
    abort(404)
if not can_review_record(user, record):
    abort(403)
```

### Pattern: Allowlist validation
```python
decision = request.form.get("decision", "")
if decision not in {"Approved", "Rejected"}:
    abort(400)
```

### Pattern: Safe update with state check
```python
cursor = db.execute(
    "UPDATE records SET status = ?, reviewed_by = ? WHERE id = ? AND status = 'Pending'",
    (decision, user["id"], record_id)
)
db.commit()
if cursor.rowcount != 1:
    abort(409)
```

### Pattern: Safe error handling
```python
try:
    # ... database operation ...
except Exception:
    app.logger.exception("Operation failed")
    return render_template("error.html", error="Something went wrong. Please try again."), 500
```

---

## Last-Minute Checklist

Before the test, make sure you can:

- [ ] Explain why "working code" can still be insecure
- [ ] Identify what crosses a trust boundary
- [ ] Explain why server-side validation is required (not just client-side)
- [ ] Write an allowlist validation for a predictable field
- [ ] Write a parameterised query with `?` placeholders (and show the tuple)
- [ ] Explain the difference between validation and output encoding
- [ ] Write safe error handling (try/except + logger + friendly message)
- [ ] Unpack `get_current_user()` correctly and use `user["role"]` etc.
- [ ] Write the full approval route flow (6 steps)
- [ ] Explain why hidden fields are not trusted security data
- [ ] Explain what a race condition is and how to prevent it
- [ ] List 4+ security-focused code review questions
- [ ] Write 4+ verification test cases (allowed + blocked)
- [ ] Explain what NIST SSDF is and its 4 practice groups
- [ ] Map an activity to the correct SDLC checkpoint
- [ ] Do a defect escape analysis (what failed, which checkpoint, what improvement)
- [ ] Write a strong security requirement (who, what, what must be blocked)
- [ ] Distinguish code review questions from release checklist items

Good luck! 🎓
