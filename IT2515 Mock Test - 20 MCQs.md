# IT2515 Mock Test — 20 MCQs
### Chapters 1–5 | 20 Marks | 15 Minutes

> **Instructions:**
> - 20 multiple choice questions
> - No calculation questions
> - All questions based on OS theory (Chapters 1–5)
> - Time yourself: 15 minutes
> - Answers are hidden — click to reveal

---

## Questions

### Q1.
Which of the following best describes the relationship between application software and system software?

A) Application software provides an interface with hardware, while system software lets users perform tasks
B) System software provides a platform for running programs and maintains system efficiency, while application software lets users perform intended tasks
C) Application software is more important than system software for the functioning of a computer
D) System software and application software are the same thing

---

### Q2.
A student claims that without an operating system, a computer can still run application programs directly. Which response is correct?

A) Yes, because application programs can access hardware directly
B) Yes, because the OS is optional software
C) No, because the OS is needed to provide resource abstractions and manage hardware access for application programs
D) No, because the OS contains the application programs themselves

---

### Q3.
Consider a university's time-sharing computing system where 50 students are logged in simultaneously. What makes this system time-sharing rather than batch processing?

A) Each student's job is stored on disk and processed in sequence overnight
B) The system uses multiprogramming to give each user the illusion of having their own console, optimizing response time
C) The system can only handle one user at a time
D) The system does not use multiprogramming

---

### Q4.
In the context of resource abstraction, which statement is TRUE?

A) Abstraction increases flexibility but makes usage more complex
B) Abstraction simplifies usage but limits flexibility
C) Abstraction eliminates the need for hardware
D) Abstraction is only used for memory management

---

### Q5.
A whiteboard in a classroom can be divided into sections for different groups. This is an example of:

A) Time-multiplexed sharing
B) Space-multiplexed sharing
C) Multiprogramming
D) Virtual memory

---

### Q6.
The kernel of an operating system executes in supervisor mode because:

A) It needs to execute user-level applications efficiently
B) It needs access to all machine instructions and all memory locations for secure operation
C) It needs to run faster than user programs
D) User programs need to verify its operations

---

### Q7.
What is the primary difference between a system call and message passing as methods of invoking OS services?

A) System calls use messages, while message passing uses function calls
B) System calls allow the user process to execute privileged instructions via a trap, while message passing has the kernel execute the function directly
C) Message passing is more efficient than system calls
D) There is no difference between them

---

### Q8.
Why are I/O and memory instructions classified as privileged instructions?

A) They are too simple for user programs to use
B) They can only be executed in assembly language
C) They directly control hardware resources, and allowing user programs to execute them directly would bypass security and protection
D) They take longer to execute than other instructions

---

### Q9.
In the von Neumann architecture, which component is responsible for decoding stored instructions and signaling the ALU to execute them?

A) Primary Memory Unit
B) Control Unit
C) Arithmetic-Logical Unit (ALU)
D) DMA Controller

---

### Q10.
During the fetch-execute cycle, what happens immediately after an instruction is fetched from memory and loaded into the Instruction Register (IR)?

A) The instruction is executed by the ALU
B) The Program Counter is incremented
C) The processor switches to user mode
D) An interrupt is generated

---

### Q11.
A device controller reports busy=1 and done=0. What can be inferred about the device?

A) The device is idle and available
B) The device has finished its operation
C) The device is currently working on an operation
D) The device has encountered an error

---

### Q12.
Direct Memory Access (DMA) is used to:

A) Allow the CPU to process I/O requests faster
B) Enable the DMA controller to read/write data from/to memory without CPU intervention, freeing the CPU for other tasks
C) Eliminate the need for device controllers
D) Replace the need for interrupts

---

### Q13.
In a multi-threaded process, which of the following is shared among all threads?

A) Program counter
B) Stack space
C) Program code and data
D) Processor registers

---

### Q14.
A context switch between two processes can occur:

A) At any point during user program execution
B) Only when the OS gains control of the CPU through traps or interrupts
C) Only when a process voluntarily yields the CPU
D) Only during I/O operations

---

### Q15.
Process Control Blocks (PCBs) are organized in the OS as:

A) Arrays indexed by process ID
B) Queues (e.g., ready queue, wait queues)
C) Trees sorted by priority
D) Hash tables

---

### Q16.
Which of the following is a benefit of demand paging over pre-loading all pages into memory?

A) It guarantees no page faults will occur
B) It avoids reading pages that may not be used, decreasing swap time and memory needed
C) It eliminates the need for a page table
D) It always runs faster than pre-loading

---

### Q17.
The valid-invalid bit in a page table entry serves to:

A) Check if the page contains valid data
B) Distinguish between pages that are in memory (valid=1) and pages on disk (invalid=0)
C) Indicate if the page has been modified
D) Mark pages that should never be replaced

---

### Q18.
A process is considered to be thrashing when:

A) It has too many threads running simultaneously
B) It spends more time paging (handling page faults) than executing actual instructions
C) It is using too much CPU time
D) It has been running for too long

---

### Q19.
In a demand-paged memory system, the page fault rate is 0.01, memory access time is 100 nanoseconds, and page fault service time is 8 milliseconds. The EAT is approximately:

A) 100 nanoseconds
B) 108 nanoseconds
C) 80,100 nanoseconds
D) 8,000,100 nanoseconds

---

### Q20.
Locality of reference is the principle that:

A) All programs execute all their code equally
B) Programs tend to execute in a few fragments of code and reference the same set of data structures at any given time
C) Programs always access memory randomly
D) Programs only use memory during initialization

---

# ═══════════════════════════════════════════
# ANSWERS (Click each to reveal)
# ═══════════════════════════════════════════

<details>
<summary>Q1 Answer</summary>

**B)** System software provides a platform for running programs and maintains system efficiency, while application software lets users perform intended tasks.

System software provides an interface with hardware and serves as a platform. Application software allows users to perform intended tasks (productivity tools, etc.). System software is independent of individual applications but common to all.

</details>

<details>
<summary>Q2 Answer</summary>

**C)** No, because the OS is needed to provide resource abstractions and manage hardware access for application programs.

The OS acts as an intermediary between user programs and hardware. Without it, there is no abstraction, no resource management, and no way for application programs to access hardware safely.

</details>

<details>
<summary>Q3 Answer</summary>

**B)** The system uses multiprogramming to give each user the illusion of having their own console, optimizing response time.

Timesharing uses multiprogramming, supports interactive computing (illusion of multiple consoles), and optimizes response time. Batch processing processes jobs sequentially offline with no human interaction.

</details>

<details>
<summary>Q4 Answer</summary>

**B)** Abstraction simplifies usage but limits flexibility.

Resource abstraction hides the actual tasks needed to manage resources, making it easy for programs to use them. However, this simplification limits what operations can be performed — some low-level operations become impossible.

</details>

<details>
<summary>Q5 Answer</summary>

**B)** Space-multiplexed sharing.

The whiteboard is divided into distinct units (sections), each allocated to different groups simultaneously. This is the definition of space-multiplexed sharing — the resource is divided and parts are allocated to different users at the same time.

</details>

<details>
<summary>Q6 Answer</summary>

**B)** It needs access to all machine instructions and all memory locations for secure operation.

The kernel is the trusted part of the OS. In supervisor mode, it can execute all instructions (including privileged ones like I/O) and access all memory (system space + user space). This is essential for controlling resources and maintaining security.

</details>

<details>
<summary>Q7 Answer</summary>

**B)** System calls allow the user process to execute privileged instructions via a trap, while message passing has the kernel execute the function directly.

In a system call, the user process/thread gains the ability to execute privileged instructions (via trap). In message passing, the kernel process/thread executes the function. System calls are more efficient because they only require a trap instruction, while message passing has overhead from message formation/copying and process multiplexing.

</details>

<details>
<summary>Q8 Answer</summary>

**C)** They directly control hardware resources, and allowing user programs to execute them directly would bypass security and protection.

I/O instructions control external devices, and memory instructions control what memory can be accessed. Making these privileged forces user programs to request these operations through the OS, which enforces access control and protection policies.

</details>

<details>
<summary>Q9 Answer</summary>

**B)** Control Unit.

The Control Unit contains the Fetch Unit, Decode Unit, Execute Unit, Instruction Register (IR), and Program Counter (PC). It causes a sequence of instructions stored in memory to be retrieved (fetched), decoded, and executed via the fetch-execute cycle.

</details>

<details>
<summary>Q10 Answer</summary>

**B)** The Program Counter is incremented.

In the fetch phase: instruction is retrieved from memory at the address in PC → loaded into IR → PC is incremented to point to the next instruction. Execution happens in the execute phase.

</details>

<details>
<summary>Q11 Answer</summary>

**C)** The device is currently working on an operation.

| busy | done | State |
|------|------|-------|
| 0 | 0 | Idle |
| 0 | 1 | Finished |
| 1 | 0 | Working |
| 1 | 1 | Undefined |

busy=1, done=0 means the device is working.

</details>

<details>
<summary>Q12 Answer</summary>

**B)** Enable the DMA controller to read/write data from/to memory without CPU intervention, freeing the CPU for other tasks.

DMA controllers act like mini CPUs that handle data transfers. The CPU initiates a DMA transfer and then performs other work in parallel, significantly increasing I/O performance.

</details>

<details>
<summary>Q13 Answer</summary>

**C)** Program code and data.

Threads in the same process share:
- Program code (they execute the same program)
- Data (they access the same variables)
- Resources (files, devices)

They do NOT share: program counter, stack space, processor registers, status (each thread has its own execution context).

</details>

<details>
<summary>Q14 Answer</summary>

**B)** Only when the OS gains control of the CPU through traps or interrupts.

Context switches require the OS to save the current process state and load another process's state. This can only happen when the OS has control of the CPU, which occurs through traps (system calls, errors) or interrupts (I/O completion, timer).

</details>

<details>
<summary>Q15 Answer</summary>

**B)** Queues (e.g., ready queue, wait queues).

PCBs are organized in queues — the ready queue holds PCBs of processes in Ready state, and wait queues hold PCBs of processes waiting for specific events/resources. Each queue is typically a linked list of PCBs.

</details>

<details>
<summary>Q16 Answer</summary>

**B)** It avoids reading pages that may not be used, decreasing swap time and memory needed.

Demand paging loads pages only when needed, not before. This means pages that won't be used aren't loaded, saving swap time and allowing more programs to fit in memory.

</details>

<details>
<summary>Q17 Answer</summary>

**B)** Distinguish between pages that are in memory (valid=1) and pages on disk (invalid=0).

Each page table entry has a valid-invalid bit. If set to valid (1), the page is legal and in memory. If invalid (0), the page is either not valid or valid but on disk. Access to an invalid page causes a page-fault trap.

</details>

<details>
<summary>Q18 Answer</summary>

**B)** It spends more time paging (handling page faults) than executing actual instructions.

Thrashing occurs when a process doesn't have enough pages — the page fault rate is very high, and the process spends most of its time swapping pages in and out rather than executing. CPU utilization drops, and the OS may mistakenly try to increase multiprogramming (making it worse).

</details>

<details>
<summary>Q19 Answer</summary>

**C)** 80,100 nanoseconds

```
EAT = (1 – p) × memory_access_time + p × page_fault_service_time
EAT = (1 – 0.01) × 100 + 0.01 × 8,000,000
EAT = 0.99 × 100 + 80,000
EAT = 99 + 80,000
EAT = 80,099 ns ≈ 80,100 ns
```

Note: Even a 1% page fault rate increases EAT by 800×.

</details>

<details>
<summary>Q20 Answer</summary>

**B)** Programs tend to execute in a few fragments of code and reference the same set of data structures at any given time.

Locality means that during any given phase of computation, a program works with a small portion of its code and data — not all of it. Code locality: code executes in a few fragments. Data locality: references cluster around the same data structures. As computation moves to a different phase, locality changes. This principle is what makes virtual memory and demand paging effective.

</details>

---

# ═══════════════════════════════════════════
# SCORING GUIDE
# ═══════════════════════════════════════════

| Score | Rating | Action |
|-------|--------|--------|
| 18–20 | 🟢 Excellent | You're ready. Review weak areas briefly. |
| 14–17 | 🟡 Good | Solid foundation. Review missed topics. |
| 10–13 | 🟠 Fair | Re-read the study guide for missed chapters. |
| 6–9 | 🔴 Needs Work | Focus on core concepts. Redo practice problems. |
| 0–5 | ⚫ Starting | Read the study guide end-to-end first. |

---

# ═══════════════════════════════════════════
# TOPIC DISTRIBUTION (Where Each Question Comes From)
# ═══════════════════════════════════════════

| Chapter | Questions | Topics Tested |
|---------|-----------|---------------|
| Ch1: Intro to OS | Q1, Q2, Q3, Q4, Q5 | OS role, system software, batch vs timesharing, abstraction, multiplexing |
| Ch2: OS Organization | Q6, Q7, Q8 | Kernel mode, system calls vs message passing, privileged instructions |
| Ch3: Computer Organization | Q9, Q10, Q11, Q12 | Von Neumann, fetch-execute cycle, device controller, DMA |
| Ch4: Process Management | Q13, Q14, Q15 | Thread sharing, context switching, PCB organization |
| Ch5: Virtual Memory | Q16, Q17, Q18, Q19, Q20 | Demand paging, valid-invalid bit, thrashing, EAT calculation, locality |

---

*Take this test under timed conditions. Then check your answers. Good luck!* 🎓
