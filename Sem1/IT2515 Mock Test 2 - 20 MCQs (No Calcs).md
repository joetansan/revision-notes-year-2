# IT2515 Mock Test 2 — 20 MCQs (No Calculations)
### Chapters 1–5 | 20 Marks | 15 Minutes

> **Exam Format (from lecturer's announcement):**
> 20 MCQs — Based on OS theory from Chapters 1 to 5. **No calculation questions will be tested.**
>
> **Instructions:**
> - 20 multiple choice questions, zero calculations
> - All questions based on OS theory (Chapters 1–5)
> - Time yourself: 15 minutes
> - Answers are hidden — click to reveal

---

## Questions

### Q1.
A new student claims that system software and application software serve the same purpose. Which of the following correctly refutes this claim?

A) System software runs faster than application software
B) System software provides an interface with hardware and a platform for running programs, while application software lets users perform specific tasks
C) Application software is installed first, then system software
D) System software is only used in servers, while application software is used on personal computers

---

### Q2.
In a multiprogramming environment, which of the following BEST explains why CPU utilization increases?

A) Programs run faster because they share the CPU
B) While one process is blocked (e.g., waiting for I/O), the CPU can execute another process
C) The CPU physically splits into multiple cores
D) Each process gets more memory when there are more processes

---

### Q3.
Consider a system that processes payroll calculations overnight without any user interaction. Jobs are prepared offline and fed to the computer as a batch. Which OS strategy is this?

A) Timesharing
B) Real-time processing
C) Batch processing
D) Personal computer processing

---

### Q4.
The operating system performs "resource abstraction." A user writes `fprintf(fileID, "%d", datum)` to save data to disk. Which statement BEST describes what the OS has done?

A) The OS has created the file physically on the disk for the first time
B) The OS has hidden the low-level operations (load, seek, out) behind a simpler function call
C) The OS has converted the program from high-level to machine language
D) The OS has allocated CPU time to the file operation

---

### Q5.
A whiteboard in a classroom is erased between different users writing on it. Each user gets the entire board for their turn. This is an example of:

A) Space-multiplexed sharing
B) Time-multiplexed sharing
C) Multiprogramming
D) Resource abstraction

---

### Q6.
The processor has two modes: supervisor and user. Which of the following can ONLY be done in supervisor mode?

A) Performing arithmetic calculations
B) Assigning values to variables
C) Executing I/O instructions and accessing system memory
D) Comparing two numbers

---

### Q7.
When a user program calls `fork()` in UNIX, the OS provides a stub function that executes a trap instruction. What is the purpose of the trap instruction?

A) To terminate the user program
B) To switch the processor from user mode to supervisor mode
C) To delete files from the hard disk
D) To create a new user account

---

### Q8.
System calls are generally more efficient than the message passing method for invoking OS services. Why?

A) System calls use faster hardware
B) System calls only require a trap instruction, while message passing has overhead from message formation, copying, and process multiplexing
C) Message passing cannot access the kernel
D) System calls do not involve the kernel

---

### Q9.
In a monolithic kernel architecture (like UNIX), all four basic managers are combined into a single software module. What is the main trade-off of this approach?

A) Better security but worse performance
B) Worse security but better performance
C) Sacrifices modularity for performance (but is harder to maintain)
D) Sacrifices performance for modularity (but is easier to maintain)

---

### Q10.
A modern computer is based on the von Neumann architecture. Which of the following correctly describes the stored program concept?

A) Programs are permanently burned into the hardware
B) Programs are stored in memory as data and can be manipulated like any other data
C) Programs must be manually loaded by the operator each time
D) Programs can only be read, never modified

---

### Q11.
During the fetch-execute cycle, the Control Unit retrieves an instruction from memory using the address in the Program Counter. What is the correct sequence of events?

A) Execute → Fetch → Decode → Increment PC
B) Fetch → Execute → Increment PC → Decode
C) Fetch (from memory[PC]) → Load into IR → Increment PC → Execute
D) Increment PC → Fetch → Execute → Load into IR

---

### Q12.
The Device Controller includes status flags: busy and done. When a device operation completes, which flag combination indicates the device is finished?

A) busy=0, done=0
B) busy=0, done=1
C) busy=1, done=0
D) busy=1, done=1

---

### Q13.
Polling and interrupts are two methods for determining I/O completion. Which statement is TRUE?

A) Polling is more efficient because it doesn't use an interrupt handler
B) Polling wastes CPU cycles because the CPU busy-waits, while interrupts allow the CPU to do other work
C) Interrupts are simpler to implement than polling
D) Polling allows the CPU to perform other tasks while waiting

---

### Q14.
A thread is sometimes called a "lightweight process." Why is this term appropriate?

A) Threads use less memory than processes
B) Threads are faster to create and switch between because they share the same address space and resources as other threads in the same process
C) Threads run on lighter hardware
D) Threads have fewer instructions than processes

---

### Q15.
Which of the following is TRUE about threads within the same process?

A) Each thread has its own program code and its own stack
B) All threads share the same program code, data, and resources, but each has its own program counter, registers, and stack
C) Each thread has its own copy of the program's data
D) Threads do not share anything with each other

---

### Q16.
A process is in the "Blocked" state. What does this mean?

A) The process is currently executing on the CPU
B) The process is waiting in the ready queue for the CPU
C) The process is waiting for some event (like I/O completion) before it can continue
D) The process has finished execution

---

### Q17.
The Process Control Block (PCB) stores all information about a process. Which of the following is NOT typically stored in a PCB?

A) Program counter and register values
B) Process state and Process ID
C) The actual program code (binary instructions)
D) Resources held and security keys

---

### Q18.
Virtual memory allows processes to execute even when they are not completely loaded into physical memory. Which principle makes this possible?

A) Programs execute all their code equally, so memory is used efficiently
B) Programs exhibit locality — they tend to execute in a few code fragments and reference the same data structures at any given time
C) All programs fit entirely in physical memory at once
D) Secondary memory is faster than primary memory

---

### Q19.
In demand paging, a page fault occurs when a process accesses a page that is not in physical memory. What is the correct sequence of events to handle a page fault?

A) Restart the program → Find the page on disk → Load into memory → Update page table
B) Find the page on disk → Find a free frame (or replace a victim) → Load page into frame → Update page table → Restart the instruction
C) Terminate the process → Reload the program → Find the page on disk
D) Ignore the page fault → The hardware will handle it automatically

---

### Q20.
A process is thrashing. The CPU utilization is very low. What is the most likely explanation?

A) The CPU is too slow for the workload
B) The process is spending most of its time swapping pages in and out of memory rather than executing actual instructions
C) The process has too many threads running
D) The process is using too much memory

---

# ═══════════════════════════════════════════
# ANSWERS (Click each to reveal)
# ═══════════════════════════════════════════

<details>
<summary>Q1 Answer</summary>

**B)** System software provides an interface with hardware and a platform for running programs, while application software lets users perform specific tasks.

System software is independent of individual applications but common to all of them. It includes the OS, compilers, libraries, and the window system. Application software (word processors, browsers, games) lets users perform intended tasks. They serve fundamentally different purposes.

</details>

<details>
<summary>Q2 Answer</summary>

**B)** While one process is blocked (e.g., waiting for I/O), the CPU can execute another process.

Multiprogramming keeps the CPU busy by switching to another runnable process when one process is blocked on I/O or waiting for resources. This increases CPU utilization without requiring the CPU to physically split or run programs faster.

</details>

<details>
<summary>Q3 Answer</summary>

**C)** Batch processing.

Batch processing uses multiprogramming, jobs are prepared offline, the OS processes jobs one after the other, there is no human-computer interaction during processing, and the OS optimizes resource utilization. Payroll processed overnight is a classic batch processing example.

</details>

<details>
<summary>Q4 Answer</summary>

**B)** The OS has hidden the low-level operations (load, seek, out) behind a simpler function call.

The progression from direct control (`load/seek/out`) to `write()` to `fprintf()` shows increasing levels of abstraction. Each level hides the complexity of the previous one, making it easier for programmers to use resources. The key idea of abstraction is simplifying usage while limiting flexibility.

</details>

<details>
<summary>Q5 Answer</summary>

**B)** Time-multiplexed sharing.

The entire resource (whiteboard) is allocated to one user for a period of time, then erased and given to the next user. This is time-multiplexed sharing — the whole resource goes to each user in turn, rather than being divided into sections (which would be space-multiplexed).

</details>

<details>
<summary>Q6 Answer</summary>

**C)** Executing I/O instructions and accessing system memory.

Privileged instructions (I/O, memory-related, processor mode-change) can ONLY execute in supervisor mode. User mode restricts programs to non-privileged instructions and user memory space. Arithmetic and comparisons are non-privileged and can run in user mode.

</details>

<details>
<summary>Q7 Answer</summary>

**B)** To switch the processor from user mode to supervisor mode.

The trap instruction switches from user mode to supervisor mode and branches to the trap table, which contains the entry points of OS system functions. The stub function executes the trap on behalf of the user program, allowing the kernel to perform the requested operation.

</details>

<details>
<summary>Q8 Answer</summary>

**B)** System calls only require a trap instruction, while message passing has overhead from message formation, copying, and process multiplexing.

System calls are more efficient because the user process/thread gains the ability to execute privileged instructions directly via a trap. Message passing requires constructing a message, sending it to the kernel process, the kernel executing the function, and sending a result back — each step adds overhead.

</details>

<details>
<summary>Q9 Answer</summary>

**C)** Sacrifices modularity for performance (but is harder to maintain).

In a monolithic kernel, all four managers (process, memory, file, device) are combined into a single module. This avoids inter-module communication overhead (better performance) but makes the system harder to maintain and debug. The trade-off is sacrificing modularity for performance.

</details>

<details>
<summary>Q10 Answer</summary>

**B)** Programs are stored in memory as data and can be manipulated like any other data.

The stored program concept (inspired by the Jacquard Loom) means that a fixed set of electronic parts can be manipulated to perform various tasks determined by a variable program. Programs are stored in primary memory alongside data, and the CPU fetches and executes instructions from memory.

</details>

<details>
<summary>Q11 Answer</summary>

**C)** Fetch (from memory[PC]) → Load into IR → Increment PC → Execute

The fetch-execute cycle:
1. Fetch: retrieve instruction from memory at address in PC
2. Load into IR
3. Increment PC to point to next instruction
4. Execute: decode and execute the instruction

This is the correct sequence. The PC is incremented during the fetch phase, not after execution.

</details>

<details>
<summary>Q12 Answer</summary>

**B)** busy=0, done=1

| busy | done | State |
|------|------|-------|
| 0 | 0 | Idle |
| 0 | 1 | Finished |
| 1 | 0 | Working |
| 1 | 1 | Undefined |

When done=1 and busy=0, the device has finished its operation and is available.

</details>

<details>
<summary>Q13 Answer</summary>

**B)** Polling wastes CPU cycles because the CPU busy-waits, while interrupts allow the CPU to do other work.

Polling requires the CPU to continuously check the device status flag, executing a busy-wait loop — wasting processor cycles. Interrupts are more efficient: the device sets an interrupt flag when done, and the CPU detects it during the fetch cycle, allowing the CPU to work on other tasks while waiting.

</details>

<details>
<summary>Q14 Answer</summary>

**B)** Threads are faster to create and switch between because they share the same address space and resources as other threads in the same process.

Threads are called "lightweight" because:
- They share code, data, and resources with other threads in the same process
- Creating a thread is cheaper than creating a process (no need to duplicate the address space)
- Context switching between threads is faster than between processes (less state to save/restore)

</details>

<details>
<summary>Q15 Answer</summary>

**B)** All threads share the same program code, data, and resources, but each has its own program counter, registers, and stack.

Shared (because they're in the same process): program code, data, resources.
Thread-specific (because each is an independent execution engine): program counter, registers, stack, status. The shared items define WHAT the process does; the thread-specific items define WHERE each thread is in that execution.

</details>

<details>
<summary>Q16 Answer</summary>

**C)** The process is waiting for some event (like I/O completion) before it can continue.

Process states:
- **Running**: Instructions being executed on CPU
- **Ready**: Waiting in queue to be assigned to CPU
- **Blocked**: Waiting for an event (I/O completion, resource allocation)
- **Done**: Finished execution

A blocked process cannot run even if the CPU is free — it must wait for its event to occur.

</details>

<details>
<summary>Q17 Answer</summary>

**C)** The actual program code (binary instructions).

The PCB stores metadata about a process: PID, program counter, register values, process state, resources held/needed, security keys, memory management info. The actual program code is stored in the process's address space (memory), not in the PCB itself. The PCB points to it but doesn't contain it.

</details>

<details>
<summary>Q18 Answer</summary>

**B)** Programs exhibit locality — they tend to execute in a few code fragments and reference the same data structures at any given time.

Locality is the principle that programs don't use all their code and data at once. During any phase, only a small portion is active. This means only those portions need to be in physical memory — the rest can stay on disk. Virtual memory exploits this by loading pages on demand, not all at once.

</details>

<details>
<summary>Q19 Answer</summary>

**B)** Find the page on disk → Find a free frame (or replace a victim) → Load page into frame → Update page table → Restart the instruction.

The correct sequence for handling a page fault:
1. The trap tells the OS a page fault occurred
2. OS determines which page is needed
3. Locate that page on disk
4. Find a free frame (or use page replacement to select a victim frame and write it out)
5. Read the desired page into the freed frame
6. Update the page and frame tables
7. Restart the instruction that caused the fault

</details>

<details>
<summary>Q20 Answer</summary>

**B)** The process is spending most of its time swapping pages in and out of memory rather than executing actual instructions.

Thrashing occurs when a process doesn't have enough page frames. The page fault rate is extremely high — the OS is constantly swapping pages in and out. The process spends more time on paging than executing, so CPU utilization drops. The OS may incorrectly think it needs more multiprogramming, making it worse.

</details>

---

# ═══════════════════════════════════════════
# SCORING GUIDE
# ═══════════════════════════════════════════

| Score | Rating | Action |
|-------|--------|--------|
| 18–20 | 🟢 Excellent | You're ready. Quick review of weak spots only. |
| 14–17 | 🟡 Good | Solid. Re-read the specific topics you missed. |
| 10–13 | 🟠 Fair | Go back to the study guide for those chapters. |
| 6–9 | 🔴 Needs Work | Redo the practice problems for missed topics. |
| 0–5 | ⚫ Starting | Read the full study guide end-to-end first. |

---

# ═══════════════════════════════════════════
# TOPIC DISTRIBUTION
# ═══════════════════════════════════════════

| Chapter | Questions | Topics Tested |
|---------|-----------|---------------|
| Ch1: Intro to OS | Q1–Q5 | System software, multiprogramming, batch/timesharing, abstraction, multiplexing |
| Ch2: OS Organization | Q6–Q9 | Privileged instructions, trap/system call, message passing vs system call, monolithic kernel |
| Ch3: Computer Organization | Q10–Q13 | Stored program, fetch-execute cycle, device controller, polling vs interrupt |
| Ch4: Process Management | Q14–Q17 | Lightweight processes, thread sharing, process states, PCB |
| Ch5: Virtual Memory | Q18–Q20 | Locality, demand paging, thrashing |

---

*No calculation questions. Pure concept understanding. Good luck!* 🎓
