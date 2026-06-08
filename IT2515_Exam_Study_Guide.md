# 📚 IT2515 Operating System & Security — Practical Test Study Guide
### Chapters 1–5 + PowerShell | 30 Marks | 40 Minutes | Closed Book

> **Test Format:**
> - **(a) 20 MCQs** — OS theory from Chapters 1 to 5. NO calculation questions. (20 marks)
> - **(b) Practical Windows PowerShell scripting** — No Linux. (10 marks)
> - **Total: 30 marks | Duration: 40 minutes**
>
> **Professor's Style:** 30 years experience. No straight definitions. Expects core concepts to be deeply understood and applied. Questions test whether you *understand* the concept, not whether you can memorize a definition.

---

## ═══════════════════════════════════════════
## UNIT 1: Introduction to Operating Systems
## ═══════════════════════════════════════════

### 1.1 What is an Operating System? ⭐⭐⭐

**Core Concept:** An OS is a program that acts as an **intermediary** between the user and the computer hardware. It provides an environment where programs can execute conveniently and efficiently. By itself, the OS performs no useful function — its value is in enabling everything else.

**Why it matters:** This is the foundational idea. The OS is not the goal — it's the enabler. Think of it like a manager who doesn't do the work but makes sure everyone else can.

**How the professor tests this:** He won't ask "Define OS." He'll ask something like:
- *"From the user's point of view, what role does the OS play?"* → It hides hardware complexity, provides a convenient interface to run programs.
- *"Can you use a computer without an OS?"* → Technically yes, but you'd need to directly control hardware (write device-level code). The OS exists because that's impractical.

---

### 1.2 System Software vs Application Software ⭐⭐

**Core Concept:**
| Type | What it does | Examples |
|------|-------------|----------|
| **Application Software** | Lets the user perform specific tasks | Word processor, browser, games |
| **System Software** | Provides interface with hardware; platform for running programs | OS, compilers, libraries, window systems, DBMS |

**Key insight:** System software is **independent of individual applications** but common to all of them. C library functions, a window system, and a DBMS are all system software.

**The Hierarchy (important for MCQs):**
```
Application Software  →  uses API
System Software       →  uses OS Interface
OS (Trusted)          →  uses Software-Hardware Interface
Hardware
```

The OS uses hardware functionality to implement the OS interface. System software uses the OS interface to export the API. Application programs use the API.

**Three perspectives:**
- **End User:** Sees application software (cut, save, print)
- **Application Programmer:** Sees system calls (malloc(), fork(), open())
- **OS Programmer:** Sees hardware operations (read-disk track, start-printer)

---

### 1.3 Resource Abstraction ⭐⭐⭐

**Core Concept:** Abstraction means the OS **hides the actual tasks** needed to manage and use resources. Users interact with simple commands instead of low-level hardware operations.

**Example from the slides — Writing to disk:**
```
Level 1 (Hardware):     load(block, length, device); seek(device, 236); out(device, 9);
Level 2 (OS write()):   write(char *block, int len, int device, int addr);
Level 3 (Application):  fprintf(fileID, "%d", datum);
```

Each level hides complexity. The application programmer just calls `fprintf()`.

**Trade-off:** Simplifies usage but **limits flexibility** — certain operations become easy while others may become impossible.

**How the professor tests this:** Expect scenarios like *"Why does the OS provide abstraction?"* or *"What happens when you write a file — what does the OS hide from you?"*

---

### 1.4 Resource Sharing ⭐⭐⭐

**Core Concept:** Two types of sharing:

| Type | How it works | Examples |
|------|-------------|----------|
| **Space-multiplexed** | Resource divided into units, each allocated to different processes | Memory (each process gets its own memory partition) |
| **Time-multiplexed** | Entire resource given to one process for a period, then switched to another | CPU (processes take turns), Printer |

**Critical for MCQs — know these scenarios:**
- A bench seat on a bus → **Space-multiplexed** (each person gets a section)
- A whiteboard in a classroom → **Either** (space if sections are assigned, time if people take turns)
- A personal computer → **Time-multiplexed** (CPU switches between processes)
- A printer on a timesharing system → **Time-multiplexed** (jobs take turns)
- A single-user file → **Time-multiplexed** (one user at a time)
- Land in a residential zone → **Space-multiplexed** (each house gets a plot)

---

### 1.5 Multiprogramming ⭐⭐⭐

**Core Concept:** A technique for sharing the CPU among runnable processes. While one process is blocked (waiting for I/O or another resource), another can run. This **increases CPU utilization**.

**Car Wash Analogy (from slides):**
- **Sequential:** One car goes through vacuum → wash → dry → vacuum inside. Next car waits.
- **Parallel (multiprogramming):** As soon as car 1 moves to wash, car 2 starts vacuum. Overlapping keeps all stations busy.

**Key point:** Multiprogramming is NOT the same as parallel processing. It's about keeping the CPU busy by switching between processes when one is waiting.

**How the professor tests this:**
- *"What factors determine the maximum number of multiprogrammed processes?"* → Memory size, I/O device availability, CPU speed, process resource requirements.
- *"How does multiprogramming increase CPU utilization?"* → By ensuring the CPU always has something to do (switches to another process when current one blocks on I/O).

---

### 1.6 OS Strategies ⭐⭐

| Strategy | Key Characteristics |
|----------|-------------------|
| **Batch Processing** | Jobs prepared offline, given to OS as a batch. No human interaction. Optimizes resource utilization. Uses multiprogramming. |
| **Timesharing** | Interactive computing. Multiple users share the system (illusion of multiple consoles). Optimizes response time. Uses multiprogramming. |
| **Personal Computer** | Single user, window-oriented |
| **Real-time/Process Control** | Timing-critical operations |
| **Distributed** | Multiple computers working together |

**Batch vs Timesharing — the key distinction:**
- Batch: No interaction, optimizes **throughput**
- Timesharing: Interactive, optimizes **response time**

---

### 1.7 Modern OS Examples ⭐

| OS | Key Facts |
|----|-----------|
| **UNIX** | Developed at AT&T Bell Labs (1970). Command-line oriented. Open OS. Time-sharing. POSIX standard. Variants: System V, BSD, HP-UX, Solaris |
| **Linux** | "Open source UNIX." By Linus Torvalds (1991) for 80386. Multiuser, multitasking. POSIX standardization |
| **Windows** | Window-oriented. Object-oriented design. Heavy use of threads. File systems: FAT, FAT32, NTFS, DFS. Active Directory. Win32 API |

---

## ═══════════════════════════════════════════
## UNIT 2: Operating System Organization
## ═══════════════════════════════════════════

### 2.1 OS Services ⭐⭐

**Two categories:**

**Services for User/Programmer Convenience:**
1. **User interface** — batch, command-line, or GUI
2. **Program execution** — load, run, terminate programs
3. **I/O operations** — file, CD/DVD, display, smartcard
4. **File-system manipulation** — create/read/write/delete files and directories, permission management
5. **Communications** — local/remote inter-process communication
6. **Error detection** — detect errors and take proper action

**Services for Efficient System Operation:**
1. **Resource allocation** — allocate resources fairly among multiple users
2. **Accounting** — track usage statistics (CPU, printer, disk quota)
3. **Protection and security** — control access to resources, audit trail

**How the professor tests this:** *"Which category does [specific service] belong to?"* or *"Give an example of a service that ensures efficient operation."*

---

### 2.2 Four Major OS Functions ⭐⭐⭐

Regardless of specific services, ALL OS have these four basic functions:

1. **Device Management** — handles generic devices (disk, tapes, terminals, printers)
2. **Process, Thread & Resource Management** — creates abstractions, allocates processor, tracks resources
3. **Memory Management** — administers primary memory, enforces isolation, enables sharing, provides virtual memory
4. **File Management** — creates abstraction of storage devices

**Key insight:** These four managers have **close interactions** with each other. They're not isolated silos.

---

### 2.3 Processor Modes ⭐⭐⭐⭐

**This is HIGH-YIELD for MCQs.**

**Core Concept:** Modern processors have **2 modes** controlled by a mode bit:

| Mode | Who runs | Capabilities |
|------|----------|-------------|
| **Supervisor Mode** (kernel mode) | OS (trusted software) | Can execute ALL instructions (including privileged), access ALL memory (system space + user space) |
| **User Mode** | User programs | Can only execute non-privileged instructions, access only user space |

**Privileged Instructions (examples):**
- I/O instructions
- Memory-related instructions
- Processor mode-change instructions

**Why this matters:** User programs must ask the OS to execute privileged instructions on their behalf. This is the foundation of OS security and resource control.

**Memory layout:**
```
┌─────────────────┐
│  Supervisor      │ ← OS space (only accessible in supervisor mode)
│  Space           │
├─────────────────┤
│  User Space      │ ← Application processes
│                  │
└─────────────────┘
```

**How the professor tests this:**
- *"In which mode does the kernel execute? Why?"* → Supervisor mode, because it needs to execute privileged instructions and access all memory.
- *"Why are I/O and memory instructions privileged?"* → Because direct access by user programs could corrupt data or compromise security. The OS must mediate all hardware access.

---

### 2.4 The Kernel ⭐⭐⭐

**Core Concept:** The kernel is the part of the OS **critical to correct operation** (trusted software). It:
- Implements basic mechanisms for secure operation
- Executes in supervisor mode
- Uses the **trap instruction** to switch from user mode to supervisor mode

---

### 2.5 System Call vs Message Passing ⭐⭐⭐⭐

**Two ways for user programs to request OS services:**

| Feature | System Call | Message Passing |
|---------|------------|-----------------|
| **How it works** | User program calls a stub → trap instruction → switches to supervisor mode → executes OS function → returns to user mode | User constructs a message → send() to kernel → kernel executes function → sends result back via receive() |
| **Who executes** | The user process/thread gains ability to execute privileged instructions (temporarily) | The kernel process/thread executes the function |
| **Efficiency** | More efficient (just a trap command) | Less efficient (message formation, copying, process multiplexing) |
| **Used by** | Most modern systems | Less common |

**System Call Flow:**
```
User calls fork()
  → stub function executes trap instruction
    → trap table consulted → finds sys_fork() address
      → sys_fork() executes in supervisor mode
        → returns to user mode, control back to user process
```

**Key point:** The trap table is crucial — it maps trap numbers to OS function entry points.

**How the professor tests this:**
- *"What are the factors that differentiate a normal procedure call from a system call?"* → Mode switch (user→supervisor→user), trap table lookup, privilege level change. A normal call doesn't involve any of this.
- *"Why are system calls more efficient than message passing?"* → No message formation/copying overhead, no process multiplexing.

---

### 2.6 Modern OS Architecture ⭐⭐⭐

| Architecture | Description | Example |
|-------------|-------------|---------|
| **Modular** | Each manager in its own module, interaction via abstract data types | — |
| **Monolithic Kernel** | All four basic modules combined into a single software module. Performance over modularity. | UNIX |
| **Microkernel** | Small kernel with only essential functions. Other functions in separate modules outside kernel. | Windows NT |

**UNIX Architecture:**
```
Application Programs → Libraries → Commands
         ↓
    OS System Call Interface
         ↓
    Monolithic Kernel Module
    ├── Process Management
    ├── Memory Management
    ├── File Management
    └── Device Mgmt Infrastructure
         ↓
    Device Drivers → Hardware
```

**Windows NT Architecture:**
```
User Processes → Libraries/Subsystems
         ↓
    NT Kernel + NT Executive
    ├── Process Management
    ├── Memory Management
    ├── File Management
    └── Device Mgmt Infrastructure
         ↓
    Hardware Abstraction Layer (HAL)
         ↓
    Hardware
```

**How the professor tests this:**
- *"Suggest reasons why UNIX is a monolithic kernel"* → Performance (frequent inter-module calls would be expensive if modular), historical design choice, all functions tightly integrated.
- *"What's the trade-off between monolithic and microkernel?"* → Monolithic: faster but less modular. Microkernel: more modular, easier to maintain, but slower due to message passing between modules.

---

## ═══════════════════════════════════════════
## UNIT 3: Computer Organization
## ═══════════════════════════════════════════

### 3.1 Von Neumann Architecture ⭐⭐⭐

**Core Concept:** Nearly all modern computers are based on this architecture. It has a **fixed set of electronic parts** that can perform various tasks determined by a **variable program** (stored program concept).

**Components:**
1. **CPU** (Central Processing Unit)
   - **ALU** (Arithmetic-Logical Unit) — performs calculations
   - **Control Unit** — fetches, decodes, and executes instructions
2. **Primary Memory Unit** — stores programs and data while CPU operates on them
3. **I/O Devices** — for input, output, communications, storage
4. **Buses** — interconnect all components (address bus, data bus)

**Inspiration:** The Jacquard Loom — used patterns (programs) to weave different cloth designs (variable tasks from fixed hardware).

---

### 3.2 The ALU ⭐⭐

**Core Concept:** Think of it as a very fast calculator.

**Components:**
- **Functional Unit** — performs the actual operations
- **Registers** — very fast memory (32-64 registers, each holding 32-bit data)
  - Data registers
  - Status registers

**How computation works:**
1. Load binary values into registers
2. Perform operations using the functional unit
3. Store result back into a register
4. Save register contents back to memory

---

### 3.3 The Control Unit ⭐⭐⭐

**Core Concept:** Causes instructions to be retrieved from memory and executed. Works on the **fetch-execute cycle**.

**Components:**
- **Fetch Unit** — retrieves instruction from memory
- **Decode Unit** — decodes the instruction
- **Execute Unit** — signals ALU to execute
- **Instruction Register (IR)** — contains copy of current instruction
- **Program Counter (PC)** — contains address of NEXT instruction

**Fetch-Execute Cycle:**
```
PC = <machine start address>;
IR = memory[PC];
haltFlag = CLEAR;
while (haltFlag not SET) {
    execute(IR);
    PC = PC + sizeof(INSTRUCT);
    IR = memory[PC];  // fetch phase
}
```

**How the professor tests this:**
- *"What algorithm does the control unit follow?"* → Fetch-execute cycle. Fetch instruction at PC, load into IR, increment PC, execute IR, repeat.
- *"What are the 3 main registers used by CPU to interact with main memory?"* → MAR (Memory Address Register), MDR (Memory Data Register), CMD (Command register).

---

### 3.4 Primary Memory Unit ⭐⭐

**Interface between CPU and memory uses 3 registers:**

| Register | Purpose |
|----------|---------|
| **MAR** (Memory Address Register) | Stores address of data to read/write |
| **MDR** (Memory Data Register) | Stores data that is read or to be written |
| **CMD** (Command Register) | Stores the command to execute (e.g., "read") |

**Read operation:**
1. Load MAR with address
2. Load CMD with "read"
3. Data appears in MDR

---

### 3.5 I/O Devices and Device Controllers ⭐⭐

**Core Concept:** Each device is controlled by a **device controller** that connects the device to the system bus.

**Device Controller Interface includes:**
- Data registers
- Command registers
- Status flags: **busy**, **done**, and error code

**Status interpretation:**
```
busy=0, done=0  → idle
busy=0, done=1  → finished
busy=1, done=0  → working
busy=1, done=1  → undefined
```

**Key point:** The OS provides **abstraction** to hide differences between device controllers from programmers.

---

### 3.6 CPU-I/O Overlap ⭐⭐⭐

**Core Concept:** We want the CPU and I/O devices to work **in parallel**. While a device is performing I/O, the CPU should be doing useful work (running another process), not sitting idle.

---

### 3.7 Polling vs Interrupts ⭐⭐⭐⭐

**HIGH-YIELD for MCQs.**

| Feature | Polling | Interrupt |
|---------|---------|-----------|
| **How it works** | CPU continuously checks (polls) the device status flag | Device signals CPU via interrupt flag when done |
| **CPU involvement** | CPU is busy-waiting, wasting cycles | CPU does other work, gets notified when done |
| **Efficiency** | Wastes processor cycles | More efficient — CPU only acts when needed |
| **Complexity** | Simple to implement | More complex (interrupt handler needed) |

**Polling code:**
```
// Start I/O
busy = 1;
while ((busy == 0) && (done == 1)) wait();
// Do the I/O operation
while (busy == 1) wait();  // CPU is stuck here!
// I/O complete
done = 0;
```

**Interrupt mechanism:**
- CPU has an **"interrupt pending"** flag
- When device.busy → FALSE, interrupt pending flag is set
- Hardware tells OS that interrupt occurred
- **Interrupt handler** (part of OS) makes process ready to run

**Fetch-Execute with Interrupt:**
```
while (haltFlag not set) {
    IR = memory[PC];
    PC = PC + 1;
    execute(IR);
    if (InterruptRequest) {
        memory[0] = PC;        // Save current PC
        PC = memory[1];        // Branch to interrupt handler
    }
}
```

**How the professor tests this:**
- *"What are the 2 ways CPU can be notified of I/O completion?"* → Polling and interrupts.
- *"Why do we want CPU and I/O to overlap?"* → To maximize CPU utilization. While waiting for slow I/O, CPU can run other processes.

---

### 3.8 Direct Memory Access (DMA) ⭐⭐⭐

**Core Concept:** Normally, the CPU transfers data between device controller registers and memory. For large I/O operations, this ties up the CPU just copying data.

**DMA solution:** A DMA controller acts as a **mini CPU** that can read/write data directly to/from memory **without CPU intervention**.

**How it works:**
1. CPU starts a DMA block transfer (tells DMA controller: source, destination, size)
2. CPU goes off to do other work
3. DMA controller handles the data transfer independently
4. DMA signals CPU when complete (via interrupt)

**This significantly increases I/O performance.**

**How the professor tests this:**
- *"What is DMA? What information does the CPU need to provide?"* → Source address, destination address, transfer size, and transfer direction (read/write).

---

## ═══════════════════════════════════════════
## UNIT 4: Process Management
## ═══════════════════════════════════════════

### 4.1 What is a Process? ⭐⭐⭐

**Core Concept:** A process is a **binary program in execution**. It consists of:
- A binary program (the code)
- Data on which the program executes
- Resources required (files, devices)

**Key insight:** Multiple processes can share the **same program text** but have different data and resources. Example: 3 users running the same editor — same code, different documents.

**The journey:**
```
Algorithm (idea) → Source Program → Binary Program → Execution Engine → Process
                                                              ↓
                                                    Stack + Status + Data + Files
```

---

### 4.2 Processes vs Threads ⭐⭐⭐⭐

**HIGH-YIELD.**

| Feature | Process | Thread |
|---------|---------|--------|
| **Definition** | A program in execution | A single execution engine within a process |
| **Has own** | Address space, data, resources, code | Program counter, status, registers, stack |
| **Shares with other** | Nothing (each process is independent) | Program code, data, resources with other threads in same process |
| **Also called** | — | Lightweight process |

**Why threads? Benefits of multithreading:**
1. **Responsiveness** — one thread can handle UI while another does computation
2. **Resource sharing** — threads share memory and resources naturally
3. **Ease of allocation** — cheaper to create than processes
4. **Multiprocessor utilization** — threads can run on different CPUs

**Thread examples:**
- Web browser: one thread displays images, another retrieves data from network
- Word processor: one thread for display, one for keystrokes, one for spell-check

---

### 4.3 Single vs Multi-threaded Processes ⭐⭐

```
Single-threaded:          Multi-threaded:
┌──────────────┐         ┌──────────────┐
│ Code         │         │ Code         │
│ Data         │         │ Data         │
│ Resources    │         │ Resources    │
│ ┌──────────┐ │         │ ┌──────────┐ │
│ │ Thread 1 │ │         │ │ Thread 1 │ │
│ │ PC,Stack │ │         │ │ PC,Stack │ │
│ │ Status   │ │         │ ├──────────┤ │
│ └──────────┘ │         │ │ Thread 2 │ │
└──────────────┘         │ │ PC,Stack │ │
                         │ ├──────────┤ │
                         │ │ Thread 3 │ │
                         │ │ PC,Stack │ │
                         │ └──────────┘ │
                         └──────────────┘
```

---

### 4.4 UNIX Processes vs Windows NT Threads ⭐⭐

**UNIX:**
- Each process has its own **address space** (subdivided into text, data, stack segments)
- OS creates a **process descriptor** to manage each process
- **PID** (Process Identifier) is the user handle
- Classic UNIX processes have **no explicit notion of a thread**
- Commands: `fork()`, `exec()`, `wait()`, `ps`

**Windows NT:**
- Win32 API supports multiple threads per process
- `CreateProcess()` — creates new process with single thread
- `CreateThread()` — adds threads to current process
- `CloseHandle()`, `WaitForSingleObject()`

---

### 4.5 Process Descriptors (PCB) ⭐⭐⭐

**Core Concept:** The OS creates a data structure called the **Process Control Block (PCB)** for each process.

**PCB contains:**
- Process ID
- Program counter
- Register values
- Process state
- Type & location of resources held
- List of resources needed
- Security keys

**PCBs are organized in queues** (ready queue, waiting queue, etc.)

---

### 4.6 Context Switching ⭐⭐⭐

**Core Concept:** When the CPU switches between two processes/threads, it's called a **context switch**.

**Key points:**
- Each thread of execution is a "context"
- A context switch can **only** occur when the OS gets control through **traps or interrupts**
- During context switch: save state of current process (from registers to PCB), load state of next process (from PCB to registers)

**How the professor tests this:**
- *"When can a context switch occur?"* → Only through traps or interrupts (the OS must gain control of the CPU).

---

### 4.7 Process States ⭐⭐⭐⭐

**HIGH-YIELD.**

**Basic states:**
| State | Meaning |
|-------|---------|
| **Running** | Instructions being executed |
| **Ready** | Waiting to be assigned to a processor |
| **Blocked** | Waiting for some event (e.g., I/O completion) |
| **Done** | Finished execution |

**State Transition Diagram:**
```
        ┌─────────────────────────────────────┐
        │                                     │
        ▼           Schedule                  │
    [Start] ──────→ [Ready] ──────────→ [Running] ──────→ [Done]
                      ▲                   │    ▲
                      │                   │    │
                      │   Request         │    │
                      │   Allocate        │    │
                      │                   ▼    │
                      └──────────── [Blocked] ─┘
                                     (I/O wait)
```

**Transitions:**
- Start → Ready: Process created
- Ready → Running: Scheduler assigns CPU
- Running → Ready: Time slice expires (preemption)
- Running → Blocked: Process requests I/O or waits for event
- Blocked → Ready: I/O complete or event occurs
- Running → Done: Process finishes

**Windows NT has more states:** Initialized, Standby, Ready, Running, Waiting, Transition, Terminated

**How the professor tests this:**
- Given specific states (Running, Ready, Blocked for Interrupt, Blocked for Reusable Resource, Blocked for Consumable Resource), draw the state diagram.
- *"What causes a transition from Running to Blocked?"* → The process requests something that isn't immediately available (I/O, resource).

---

### 4.8 Process Manager Responsibilities ⭐⭐

1. Define & implement process/thread characteristics (algorithms, data structures)
2. Define address space (what threads can reference)
3. Manage resources used by processes/threads
4. Create/destroy/manipulate processes & threads
5. Schedule processes on CPU
6. Thread synchronization tools
7. Deadlock handling
8. Protection mechanisms

---

## ═══════════════════════════════════════════
## UNIT 5: Virtual Memory
## ═══════════════════════════════════════════

### 5.1 Why Virtual Memory? ⭐⭐⭐

**Core Concept:** Physical memory alone isn't enough because:
1. Large portions of most programs are **not executed most of the time**
2. Only the active portions need to be in memory
3. We want to load as many programs as possible to increase CPU utilization
4. Fast secondary memory (hard disk) can supplement primary memory

**Virtual memory allows:** Execution of processes that are **not completely in memory**. Programs larger than physical memory can run.

---

### 5.2 Locality ⭐⭐⭐

**Core Concept:** Every process has **code and data locality**:
- Code tends to execute in **a few fragments** at a time
- Programs tend to reference the **same set of data structures**
- As computation moves to a different phase, locality changes

**Example — Address Space for a program:**
```
Initialization code     → used once, <1% execution time
Code for phase 1 (Φ1)   → 30% execution time
Code for phase 2 (Φ2)   → 20% execution time
Code for phase 3 (Φ3)   → 35% execution time
Error handling code      → <1% execution time
Data & stack             → 15% execution time
```

**Why locality matters:** It's the reason virtual memory works. If programs randomly accessed all their code, paging would be terrible. Locality means we only need a small portion in memory at any time.

**How the professor tests this:**
- *"Explain code and data locality in your own words"* → Programs don't use all their code at once. They tend to execute small sections repeatedly and access the same data structures. This predictable pattern lets us keep only the active parts in memory.

---

### 5.3 Paging ⭐⭐⭐⭐

**HIGH-YIELD.**

**Core Concept:** Memory is divided into fixed-size blocks:
- **Page** — a fixed-size block of **virtual** addresses (size = 2^h)
- **Page Frame** — a fixed-size block of **physical** memory (same size as a page)

**Why power of 2?** Minimizes translation time between virtual and physical addresses (bit shifting instead of division).

---

### 5.4 Demand Paging ⭐⭐⭐⭐

**Core Concept:** The pager only brings pages into memory **when they are needed** (on demand). In pure demand paging, no page is loaded until it's accessed.

**Benefits:**
- Programs not constrained by physical memory size
- Each program takes less physical memory
- More programs can run simultaneously → higher CPU utilization

---

### 5.5 Page Fault ⭐⭐⭐⭐

**Core Concept:** A page fault occurs when a process accesses a page that is **not in primary memory** but exists in virtual memory (on disk).

**What happens during a page fault:**
1. Locate the demanded page on disk
2. Find a free frame:
   - If free frame exists → use it
   - If no free frame → use **page replacement algorithm** to select a victim, write victim to disk (only if modified/dirty), update page and frame tables
3. Read desired page into the freed frame
4. Update page and frame tables
5. Restart the user program

**Dirty bit:** A modify bit reduces overhead — only pages that were **modified** are written back to disk.

---

### 5.6 Page Table ⭐⭐⭐⭐

**Core Concept:** A hardware mechanism that maps **logical page numbers** to **physical page frame numbers**.

**Example:**
```
Logical Memory:     Page Table:        Physical Memory:
Page 0 ──────────→ Frame 2 ──────────→ Frame 0 (some other process)
Page 1 ──────────→ Frame 6            Frame 1
Page 2 ──────────→ Frame 3            Frame 2 ← Page 0 is here
Page 3 ──────────→ Frame 7            Frame 3 ← Page 2 is here
Page 4 ──────────→ Frame 5            Frame 4
Page 5 ──────────→ Frame 1            Frame 5 ← Page 4 is here
                                       Frame 6 ← Page 1 is here
                                       Frame 7 ← Page 3 is here
```

---

### 5.7 Valid-Invalid Bit ⭐⭐⭐

**Core Concept:** Each page table entry has a bit:
- **Valid (1)** = page is in memory (legal and accessible)
- **Invalid (0)** = page is NOT in memory (either not valid, or valid but on disk)

**Access to an invalid page → page fault trap.**

---

### 5.8 Effective Access Time (EAT) ⭐⭐

**Formula (know the concept, even though no calculations on test):**
```
EAT = (1 – p) × memory_access_time + p × (page_fault_overhead + swap_out + swap_in + restart_overhead)
```
Where p = page fault rate (0 ≤ p ≤ 1)

**Key insight:** EAT is **directly proportional** to page fault rate. Even a tiny increase in page fault rate dramatically slows things down because servicing a page fault (disk I/O) is ~10,000× slower than memory access.

---

### 5.9 Page Replacement ⭐⭐

When no free frames exist, the OS must select a **victim frame** to replace. Common algorithms (know they exist):
- FIFO (First In, First Out)
- LRU (Least Recently Used)
- Optimal (theoretical best)

**Dirty bit optimization:** Only write back pages that were modified (dirty). Unmodified pages can simply be overwritten.

---

### 5.10 Thrashing ⭐⭐⭐⭐

**HIGH-YIELD.**

**Core Concept:** If a process doesn't have "enough" pages, page fault rate becomes very high. **Thrashing** = a process spends more time **paging** than **executing**.

**Symptoms:**
- CPU utilization is very low
- OS may think it needs more multiprogramming (adding more processes makes it WORSE)

**Why does thrashing occur?**
- Σ size of localities > total memory size
- Not enough memory to hold the working sets of all processes

**Solution:** Use a **local (or priority) replacement algorithm** — each process only replaces its own pages, preventing one process from stealing frames from another.

**Why does paging work (when thrashing doesn't occur)?**
- **Locality model** — processes migrate between localities, localities may overlap, but at any time only a small portion is needed

**How the professor tests this:**
- *"What is the cause of thrashing?"* → Process doesn't have enough pages, so it keeps page-faulting.
- *"How does the system detect thrashing?"* → Low CPU utilization despite high multiprogramming level.
- *"What can the system do?"* → Use local replacement, reduce degree of multiprogramming, or allocate more frames to the process.

---

## ═══════════════════════════════════════════
## UNIT 6: Windows PowerShell Scripting (10 marks)
## ═══════════════════════════════════════════

### 6.1 PowerShell Basics ⭐⭐⭐

**Key differences from traditional shells:**
- PowerShell is **object-oriented** (not text-based)
- Cmdlets are **.NET Framework classes**, not standalone executables
- Pipes pass **objects**, not text streams
- Parsing, error handling, and output formatting are handled by the PowerShell runtime
- **Not case-sensitive**

---

### 6.2 Redirection Operators ⭐⭐⭐

| Operator | What it does | If file exists with data |
|----------|-------------|------------------------|
| `>` | Writes (overwrites) output to file | **Overwrites** existing data |
| `>>` | **Appends** output to file | **Adds to end** of existing data |

**How the professor tests this:** *"Explain the operational difference between > and >>. What happens if the target file already contains data?"*

---

### 6.3 Pipeline Operator `|` ⭐⭐⭐

**Core Concept:** Passes the **output object** from one cmdlet as **input** to the next cmdlet.

```powershell
Get-Process | Sort-Object
# Gets all processes, then sorts them
```

**Key point:** In PowerShell, this passes objects (not text). The receiving cmdlet can access all properties and methods of the passed object.

---

### 6.4 Comparison Operators ⭐⭐⭐⭐

**CRITICAL — PowerShell does NOT use == or < or >**

| Standard Math | PowerShell | Meaning |
|--------------|------------|---------|
| `==` | `-eq` | Equal to |
| `!=` | `-ne` | Not equal to |
| `>` | `-gt` | Greater than |
| `<` | `-lt` | Less than |
| `>=` | `-ge` | Greater than or equal to |
| `<=` | `-le` | Less than or equal to |
| pattern | `-like` | Wildcard pattern matching |

**How the professor tests this:** *"State the correct PowerShell comparison operators for: Equals to, Not equal to, Greater than, Less than or equal to"* → `-eq`, `-ne`, `-gt`, `-le`

---

### 6.5 Error Handling ⭐⭐⭐

**Core Concept:** When `Get-Service` queries a non-existent service, it produces an error that halts clean output.

**Solution:** Use the `-ErrorAction` parameter to suppress this behavior.

```powershell
$service = Get-Service -Name "NonExistent" -ErrorAction SilentlyContinue
if ($service) {
    Write-Host "Service found"
} else {
    Write-Host "Service not found"
}
```

`-ErrorAction SilentlyContinue` suppresses the error, allowing the `If-Else` block to gracefully handle missing items.

---

### 6.6 Variables ⭐⭐

```powershell
$name = "Hello"          # Variable names start with $
[int]$number = 5         # Type casting with square brackets
[string]$text = "World"  # .NET types
```

**Variable types:** `[datetime]`, `[string]`, `[char]`, `[double]`, `[single]`, `[int]`, `[boolean]`

**Boolean:** Zero = false, any non-zero number = true.

**Double quotes:** Variable names are replaced with their values.
**Single quotes:** Variable names are treated as literal text.

**Escape character:** Backtick `` ` `` (not backslash!)
- `` `n `` = newline, `` `t `` = tab, `` `r `` = carriage return

---

### 6.7 Arrays and Loops ⭐⭐⭐

**Array creation:**
```powershell
$array = 1, 3, 5, 7, 9    # Array with 5 odd numbers
```

**Foreach loop:**
```powershell
$array = 1, 3, 5, 7, 9
foreach ($item in $array) {
    echo $item
}
```

**Other loops:** `for`, `while`, `do-while`

---

### 6.8 If-ElseIf-Else ⭐⭐⭐

```powershell
[int]$number = Read-Host "Enter a number (1 to 10)"
if ($number -gt 10) {
    Write-Host "The number is greater than 10"
} elseif ($number -lt 1) {
    Write-Host "The number is less than 1"
} else {
    Write-Host "The number is within the range 1 to 10"
}
```

**Key pitfall:** Must cast input to `[int]` — otherwise string comparison gives wrong results (e.g., "5" is greater than "10" in string comparison).

---

### 6.9 Useful Cmdlets ⭐⭐

| Cmdlet | Purpose |
|--------|---------|
| `Get-Help` | Get help on commands |
| `Get-Command` | List all available commands |
| `Get-Member` | List methods and properties of an object |
| `Get-ChildItem` | Get items and child items in a location |
| `Where-Object` | Filter data returned by other cmdlets |
| `Read-Host` | Read input from console |
| `Get-Content` | Read file content |
| `Write-Host` | Output to console |
| `Clear-Host` / `cls` | Clear console |
| `Get-ExecutionPolicy` | Check script execution policy |
| `Set-ExecutionPolicy` | Set execution policy |

---

### 6.10 Execution Policy ⭐⭐

Scripts may fail if execution policy isn't set. Fix:
```powershell
Set-ExecutionPolicy RemoteSigned
```

---

### 6.11 Practice Script Pattern (Likely Exam Format) ⭐⭐⭐

Based on the revision paper, expect something like:

**Create an array, loop through it, print each element:**
```powershell
# Revision.ps1
$array = 1, 3, 5, 7, 9
foreach ($item in $array) {
    echo $item
}
```

**Or: Read from file, process with conditions:**
```powershell
$items = Get-Content data.txt
foreach ($item in $items) {
    if ($item -gt 10) {
        Write-Host "$item is greater than 10"
    } else {
        Write-Host "$item is 10 or less"
    }
}
```

---

## ═══════════════════════════════════════════
## 🎯 QUICK-FIRE MCQ REVISION (Self-Test)
## ═══════════════════════════════════════════

Test yourself on these. Cover the answer, try to recall, then check.

1. **What is an OS?** → Intermediary between user and hardware; provides environment for program execution
2. **System software vs application software?** → System: interface with hardware (OS, compilers). Application: user tasks (word, browser)
3. **What is abstraction?** → OS hides hardware complexity behind simple commands
4. **Memory is space-multiplexed or time-multiplexed?** → Space-multiplexed (each process gets its own partition)
5. **CPU is space-multiplexed or time-multiplexed?** → Time-multiplexed (processes take turns)
6. **What does multiprogramming do?** → Shares CPU among processes; while one blocks on I/O, another runs
7. **Batch vs timesharing?** → Batch: no interaction, optimizes throughput. Timesharing: interactive, optimizes response time
8. **What are the 4 OS functions?** → Device, Process/Thread/Resource, Memory, File management
9. **Supervisor mode vs User mode?** → Supervisor: all instructions, all memory. User: non-privileged only, user space only
10. **What are privileged instructions?** → I/O, memory-related, mode-change instructions
11. **What is the kernel?** → Trusted part of OS, executes in supervisor mode
12. **System call vs message passing?** → System call: trap instruction, user process gains privilege. Message passing: kernel process executes function
13. **Why are system calls more efficient?** → No message formation/copying, just a trap command
14. **Monolithic vs microkernel?** → Monolithic: all in one module (UNIX). Microkernel: minimal kernel, rest in modules
15. **Von Neumann architecture components?** → CPU (ALU + CU), Primary Memory, I/O Devices, Buses
16. **What does the control unit do?** → Fetch-decode-execute cycle
17. **PC and IR?** → PC: address of next instruction. IR: copy of current instruction
18. **MAR, MDR, CMD?** → Memory Address Register, Memory Data Register, Command register
19. **Polling vs Interrupt?** → Polling: CPU busy-waits. Interrupt: device signals CPU
20. **What is DMA?** → Direct Memory Access; controller transfers data without CPU intervention
21. **What is a process?** → Binary program in execution (code + data + resources)
22. **Thread vs process?** → Thread: execution engine within a process. Shares code/data/resources with other threads
23. **What is a PCB?** → Process Control Block: data structure storing process state, PC, registers, resources
24. **When can context switching occur?** → Only through traps or interrupts
25. **Process states?** → Running, Ready, Blocked, Done
26. **What causes Running→Blocked?** → Process waits for I/O or resource
27. **What is virtual memory?** → Allows execution of processes not completely in memory; uses disk to extend RAM
28. **What is locality?** → Programs use only small portions of code/data at any time
29. **Page vs page frame?** → Page: block of virtual addresses. Frame: block of physical memory (same size)
30. **What is demand paging?** → Load pages only when needed
31. **What is a page fault?** → Accessing a page not in memory
32. **Valid vs invalid bit?** → Valid(1): in memory. Invalid(0): not in memory
33. **What is thrashing?** → Process spends more time paging than executing
34. **Cause of thrashing?** → Not enough pages; Σ locality > memory size
35. **PowerShell: == operator?** → `-eq` (not ==)
36. **PowerShell: > operator?** → `-gt`
37. **> vs >> in PowerShell?** → > overwrites, >> appends
38. **Pipeline | does what?** → Passes object output from one cmdlet to next
39. **-ErrorAction SilentlyContinue?** → Suppresses errors, allows graceful handling
40. **How to create array in PowerShell?** → `$array = 1, 3, 5, 7, 9`

---

## ═══════════════════════════════════════════
## 📝 REVISION PAPER ANSWERS
## ═══════════════════════════════════════════

From the official revision paper:

**Q1. Redirection Operators (4 marks)**
- `>` operator: **Overwrites** the target file. If file already contains data, all existing data is **replaced**.
- `>>` operator: **Appends** to the target file. If file already contains data, new data is **added to the end** without losing existing content.

**Q2. The Pipeline (3 marks)**
- When data passes through `|`, it is transferred as an **object** (not text) from one cmdlet to the next.
- Example: `Get-Process | Sort-Object` — Get-Process retrieves process objects, passes them through the pipeline to Sort-Object, which sorts them by property.

**Q3. Conditional Operators (4 marks)**
- Equals to: `-eq`
- Not equal to: `-ne`
- Greater than: `-gt`
- Less than or equal to: `-le`

**Q4. Error Handling (4 marks)**
- Parameter: `-ErrorAction SilentlyContinue`
- This suppresses the error when querying a non-existent service, allowing the If-Else block to check if the result is null/empty and handle the "missing" case gracefully without halting script execution.

**Q5. PowerShell Script (5 marks)**
```powershell
# Revision.ps1
$array = 1, 3, 5, 7, 9
foreach ($item in $array) {
    echo $item
}
```

---

## ═══════════════════════════════════════════
## 🔑 TOP 10 HIGH-PROBABILITY MCQ TOPICS
## ═══════════════════════════════════════════

Based on the professor's style (application-based, not definitions) and tutorial questions:

1. **Space vs Time multiplexed sharing** — given scenarios, identify which type
2. **Supervisor vs User mode** — what can each do, why is it needed
3. **Privileged instructions** — why I/O and memory instructions are privileged
4. **System call mechanism** — trap instruction, trap table, mode switching
5. **Polling vs Interrupts** — trade-offs, how each works
6. **Process states and transitions** — what causes each transition
7. **Threads vs Processes** — what's shared, what's private
8. **Context switching** — when it can occur, what happens during it
9. **Page faults** — what triggers one, what happens during service
10. **Thrashing** — cause, detection, solution

---

**Good luck on your test tomorrow! Focus on understanding WHY each concept exists, not just WHAT it is. The professor tests application of knowledge.** 💪
