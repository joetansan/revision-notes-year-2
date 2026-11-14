# 📚 IT2515 Operating Systems and Security — Practical Test Study Guide
### Chapters 1–5 + PowerShell Scripting | 30 Marks | 40 Minutes

> **Format:**
> - (a) 20 MCQs — OS theory from Chapters 1 to 5. No calculation questions. (20 marks)
> - (b) Practical Windows PowerShell scripting. No Linux scripting. (10 marks)
>
> **Professor's Pattern:** No straight definitions. Expect concept application, "why" and "how" reasoning, and connecting ideas across topics. 30 years of experience — he tests understanding, not memorization.

---

# ═══════════════════════════════════════════
# UNIT 1: INTRODUCTION TO OPERATING SYSTEMS
# ═══════════════════════════════════════════

## 1.1 What is an Operating System? ⭐

**Core Concept:**
An OS is a program that acts as an **intermediary** between the user and the computer hardware. It provides an environment for executing programs conveniently and efficiently. By itself, it performs no useful function — its value is in enabling everything else.

**Why It Matters:**
This is the foundational concept. Every other topic builds on the idea that the OS sits between hardware and user, managing resources.

**How Professor Tests This:**
- Never asks "Define OS" directly
- Instead: "From the user's point of view, what role does the OS play?" (Tutorial 1, Q1)
- Or scenario-based: "Can you use a computer without an OS?" (Tutorial 1, Q3)

**Key Insight:** The OS is **pure overhead** — it has no direct value to the end user. Application programs have the real value. But without the OS, those programs can't run.

---

## 1.2 Application Software vs System Software ⭐⭐

**Core Concept:**

| Type | Purpose | Examples |
|------|---------|----------|
| **Application Software** | Lets user perform intended tasks | Word, Browser, Games |
| **System Software** | Provides interface with hardware; platform for running programs | OS, Compilers, DBMS, Window System, Libraries |

System software provides **two environments**:
1. Allows human users to interact with the computer
2. Provides tools/subassemblies for application programs

**The Hierarchy:**
```
Application Software  →  Human-Computer Interface
        ↑ API
System Software       →  OS Interface
        ↑
OS (Trusted)          →  Software-Hardware Interface
        ↑
Hardware Resources
```

**How Professor Tests This:**
- "List any 3 components of system software" (Tutorial 1, Q2)
- MCQ: Given a list, identify which are application vs system software
- Understanding that system software is **independent of individual applications** but common to all

---

## 1.3 Resource Abstraction ⭐⭐⭐

**Core Concept:**
Abstraction is when the OS **hides the actual tasks** needed to manage and use resources. Users programs use simpler commands instead of dealing with hardware directly.

**The Disk Write Example (from slides):**
```
Without abstraction:  load(block, length, device); seek(device, 236); out(device, 9);
With write():         write(char *block, int len, int device, int addr);
With fprintf():       fprintf(fileID, "%d", datum);
```

Each layer of abstraction makes things simpler but limits flexibility — certain operations become easy while others may become impossible.

**Why It Matters:**
This is THE core concept of OS design. Everything the OS does — process management, memory management, file management, device management — is about creating abstractions.

**How Professor Tests This:**
- MCQ: Given a scenario, identify which level of abstraction is being used
- "Explain abstraction in terms of an OS managing resources" (Tutorial 2, Q1)
- Connecting abstraction to resource sharing

---

## 1.4 Resource Sharing ⭐⭐

**Core Concept:**
Two kinds of sharing:

| Type | What Happens | Examples |
|------|-------------|----------|
| **Space-multiplexed** | Resource divided into distinct units, each allocated to different processes | Memory (each process gets its own memory space) |
| **Time-multiplexed** | Entire resource allocated to one process for a period, then given to another | CPU (processes take turns), Printer |

**How Professor Tests This:**
- "Identify which are space-multiplexed and which are time-multiplexed" (Tutorial 1, Q4)
- Examples given: land in residential zone (space), personal computer (time), whiteboard (either), bench seat on bus (space), single-user file (time), printer on timesharing (time)

**Key Insight:** Some resources could be **either** strategy depending on context. A whiteboard can be divided into sections (space) or shared by erasing between users (time).

---

## 1.5 Multiprogramming ⭐⭐⭐

**Core Concept:**
Multiprogramming is the technique for **sharing the CPU among runnable processes**. When one process is blocked (waiting for I/O or another resource), another process can use the CPU. This increases CPU utilization.

**The Car Wash Analogy:**
- Sequential: One car goes through vacuum → wash → dry → vacuum inside. Next car waits.
- Parallel: While Car 1 is drying, Car 2 starts washing. Much more efficient.

**How It Works:**
1. Process may be blocked on I/O
2. Process may be blocked waiting for CPU
3. While one process is blocked, another can run
4. OS schedules processes automatically

**How Professor Tests This:**
- "What factors determine maximum number of multiprogrammed processes?" (Tutorial 1, Q5)
- MCQ: Understanding that multiprogramming increases CPU utilization
- Connecting multiprogramming to both batch and timesharing systems

---

## 1.6 OS Strategies ⭐⭐

**Core Concept:**

| Strategy | Key Characteristic | Use Case |
|----------|-------------------|----------|
| **Batch Processing** | Jobs prepared offline, processed sequentially, no human interaction | Payroll, end-of-day reports |
| **Timesharing** | Interactive computing, multiple users, optimizes response time | Multi-user servers, university systems |
| **Personal Computer** | Single user, window-oriented | Desktop/laptop |
| **Real-time/Process Control** | Time-critical responses | Industrial control, embedded systems |

**Batch Processing:** Uses multiprogramming, jobs given as a batch, OS optimizes resource utilization, no human-computer interaction.

**Timesharing:** Uses multiprogramming, supports interactive computing (illusion of multiple consoles), different scheduling/memory strategies than batch, optimizes response time, pays considerable attention to resource isolation (security & protection).

**How Professor Tests This:**
- "When is batch preferred vs timesharing?" (Tutorial 1, Q6)
- MCQ: Given a scenario, identify which OS strategy is most appropriate

---

## 1.7 Modern OS Examples ⭐

| OS | Key Facts |
|----|-----------|
| **UNIX** | Developed by AT&T Bell Labs 1970, command-line oriented, open OS, POSIX.1 standard, timesharing |
| **Linux** | "Open source UNIX" by Linus Torvalds 1991 for 80386, multiuser/multitasking, POSIX standardization |
| **Windows** | Object-oriented design, heavy use of threads, FAT/NTFS/DFS file systems, Active Directory, Win32 API |

---

# ═══════════════════════════════════════════
# UNIT 2: OPERATING SYSTEM ORGANIZATION
# ═══════════════════════════════════════════

## 2.1 OS Services ⭐⭐

**Two Categories:**

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
3. **Protection and security** — security from outsiders, controlled access, audit trail

**How Professor Tests This:**
- MCQ: "Which of the following is a service for user convenience vs system efficiency?"
- Understanding the distinction between the two categories

---

## 2.2 Four Major OS Functions ⭐⭐⭐

Every OS implements **4 major managers**:

| Manager | What It Does |
|---------|-------------|
| **Process, Thread & Resource Manager** | Creates abstractions of processes/threads/resources, allocates processor, tracks abstract resources (queues, semaphores, messages) |
| **Memory Manager** | Administers/allocates primary memory, enforces isolation, enables sharing, provides virtual memory |
| **Device Manager** | Handles generic devices (disk, tapes, terminals, printers), special approaches for CPU and memory |
| **File Manager** | Creates abstraction of storage devices, byte stream to indexed records, local and remote file systems |

**Key Point:** These four managers have **close interactions** with each other.

---

## 2.3 Key OS Requirements ⭐⭐

The OS must:
1. **Manage resource sharing** — time/space-multiplexing where appropriate
2. **Allow exclusive use** — let processes use a resource exclusively when needed
3. **Ensure isolation** — protect information from being modified or tampered with
4. **Managed sharing** — sharing must be orderly according to resource properties (printer vs disk drive)

---

## 2.4 Implementation Mechanisms ⭐⭐⭐

Three basic mechanisms to address isolation and sharing:

### 2.4.1 Processor Modes ⭐⭐⭐

**Core Concept:**
Modern processors provide **2 modes** controlled by a **mode bit**:

| Mode | Who Uses It | Capabilities |
|------|------------|-------------|
| **Supervisor Mode** | OS (trusted software) | Execute ALL instructions (including privileged), access ALL memory (system space + user space) |
| **User Mode** | User programs | Execute only non-privileged instructions, access only user space |

**Privileged Instructions (can ONLY run in supervisor mode):**
- I/O instructions
- Memory-related instructions
- Processor mode-change instructions

**Why This Matters:**
This is how the OS maintains control. User programs must ask the OS to execute privileged instructions on their behalf. The administrator's policy determines what gets isolated vs shared.

**How Professor Tests This:**
- "In which mode does the kernel execute? Why?" (Tutorial 2, Q2)
- MCQ: Given a scenario, determine which mode is needed
- "Why are I/O and memory instructions privileged?" (Tutorial 2, Q5)

**Key Insight:** I/O and memory instructions are privileged because they directly affect hardware resources. If user programs could execute them directly, they could bypass security, corrupt memory, or interfere with other processes.

---

### 2.4.2 The Kernel ⭐⭐⭐

**Core Concept:**
The kernel is the part of the OS **critical to correct operation** (trusted software). It:
- Implements basic mechanisms for secure operation
- Executes in **supervisor mode**
- Uses the **trap instruction** to switch from user to supervisor mode

**How Professor Tests This:**
- MCQ: "What is the role of the kernel?"
- "Suggest reasons why UNIX is a monolithic kernel" (Tutorial 2, Q4)

---

### 2.4.3 Invoking System Services ⭐⭐⭐

**Two Techniques:**

#### System Call
1. User program calls a **stub function** provided by the OS
2. Stub switches processor to **supervisor mode**
3. Executes **trap instruction** → branches to **trap table** → finds entry point of system function
4. System function executes in kernel
5. On completion, processor switches back to **user mode**, control returns to user process
6. Appears as an ordinary function call to the programmer

#### Message Passing
1. User program constructs a **message** requesting the desired service
2. Uses OS **send()** system call
3. OS kernel implements the target function
4. User process waits with **receive()** operation
5. Kernel sends message back on completion

**Comparison:**

| Feature | System Call | Message Passing |
|---------|------------|----------------|
| Who executes? | User process/thread gains ability to execute privileged instructions | Kernel process/thread executes the function |
| Efficiency | More efficient — just requires a trap command | Less efficient — message formation/copying and process multiplexing overhead |
| Used by | Most modern systems | Fewer systems |

**How Professor Tests This:**
- "What factors differentiate a normal procedure call from a system call?" (Tutorial 2, Q3)
- MCQ: Steps in a system call, role of trap table
- Understanding that system calls are more efficient than message passing

**Key Insight:** The trap table is crucial — it maps trap numbers to the actual kernel function addresses. Without it, the system wouldn't know which function to execute.

---

## 2.5 Modern OS Architecture ⭐⭐

| Architecture | Description | Example |
|-------------|-------------|---------|
| **Modular** | Each manager in its own software module, interaction via abstract data types | Theoretical ideal |
| **Monolithic** | All four basic modules combined into a single software module | UNIX |
| **Microkernel** | Small kernel with only essential/critical functions, remaining functions outside kernel in separate modules | Mach, Windows NT (hybrid) |

**Trade-off:** Modular is cleaner but frequent inter-module calls incur performance penalty. Monolithic sacrifices modularity for performance.

**Windows NT Organization:**
```
User Space:      Processes → Subsystems → Libraries
                      ↕ (T = trap)
Supervisor:      NT Kernel + NT Executive
                 (Process Mgmt, Memory Mgmt, File Mgmt, Device Mgmt, I/O Subsystem)
                      ↕
Hardware:        Hardware Abstraction Layer (HAL) → Processors, Memory, Devices
```

---

# ═══════════════════════════════════════════
# UNIT 3: COMPUTER ORGANIZATION
# ═══════════════════════════════════════════

## 3.1 Von Neumann Architecture ⭐⭐⭐

**Core Concept:**
Almost all modern computers are based on this architecture. It has a **fixed set of electronic parts** that can be manipulated to perform various tasks determined by a **variable program** (stored program concept — inspired by Jacquard Loom).

**Components:**
1. **CPU** (Central Processing Unit) — contains ALU + Control Unit
2. **Primary Memory Unit** — stores programs and data being operated on
3. **I/O Devices** — for input, output, communications, storage
4. **Buses** — interconnect components (Address Bus, Data Bus)

**How Professor Tests This:**
- "What architecture is modern computer based on? Briefly describe." (Tutorial 3, Q1)
- MCQ: Components of von Neumann architecture

---

## 3.2 The CPU (ALU + Control Unit) ⭐⭐⭐

### ALU (Arithmetical-Logical Unit)
- Performs arithmetic and logical operations
- Contains:
  - **Functional unit** — performs the operations
  - **Registers** — very fast memory (32–64 registers, each holding 32-bit data)
  - **Status registers**
- Computation cycle: Load values into registers → perform operations → store results back

### Control Unit
- Causes instructions to be **fetched and executed** in sequence
- Contains:
  - **Fetch Unit** — fetches instruction from memory
  - **Decode Unit** — decodes the instruction
  - **Execute Unit** — signals ALU to execute
  - **Instruction Register (IR)** — contains copy of current instruction
  - **Program Counter (PC)** — contains memory address of next instruction

**The Fetch-Execute Cycle:**
```
PC = <machine start address>
IR = memory[PC]
while (haltFlag not set) {
    execute(IR)
    PC = PC + sizeof(INSTRUCTION)
    IR = memory[PC]    // fetch phase
}
```

**How Professor Tests This:**
- "What algorithm does the control unit follow?" (Tutorial 3, Q2)
- MCQ: What happens during fetch phase vs execute phase
- Understanding PC and IR roles

---

## 3.3 Primary Memory Unit ⭐⭐

**Interface between CPU and memory uses 3 registers:**

| Register | Purpose |
|----------|---------|
| **MAR** (Memory Address Register) | Stores address of data to be read/written |
| **MDR** (Memory Data Register) | Stores data that is read or to be written |
| **CMD** (Command Register) | Stores the command to be executed |

**Read Operation:**
1. Load MAR with address
2. Load CMD with "read"
3. Data appears in MDR

**How Professor Tests This:**
- "What are the 3 main registers used by CPU to interact with main memory?" (Tutorial 3, Q3)
- MCQ: Given a scenario, identify which register is involved

---

## 3.4 I/O Devices and Device Controllers ⭐⭐

**Core Concept:**
Each device operation is controlled by a **device controller** which:
- Connects device to the computer's address and data bus
- Provides an interface for the OS (Device Manager) to manipulate the device
- Includes: data registers, command registers, status flags (done, busy, error code)

**Status Flags:**
| busy | done | State |
|------|------|-------|
| 0 | 0 | Idle |
| 0 | 1 | Finished |
| 1 | 0 | Working |
| 1 | 1 | Undefined |

**Why I/O Overlap Matters:**
While one process is doing I/O, the CPU can work on another process. This is fundamental to multiprogramming.

**How Professor Tests This:**
- "Why do we want CPU operation to overlap with I/O processing?" (Tutorial 3, Q4)
- MCQ: Understanding device controller interface

---

## 3.5 Determining I/O Completion ⭐⭐⭐

### Polling
- CPU **continuously checks** (polls) the device status flag
- If I/O not done, CPU executes a **busy-wait** command
- **Wastes processor cycles** — CPU is effectively doing nothing while waiting

### Interrupt
- CPU has an **interrupt pending** flag
- When device finishes (busy → FALSE), it sets the interrupt flag
- CPU, during its fetch cycle, detects the flag
- CPU branches to **interrupt handler** routine (part of OS)
- Interrupt handler makes the process ready to run
- **More efficient** — CPU can do other work while waiting

**Fetch-Execute Cycle with Interrupt:**
```
while (haltFlag not set) {
    IR = memory[PC]
    PC = PC + 1
    execute(IR)
    if (InterruptRequest) {
        memory[0] = PC          // save current PC
        PC = memory[1]          // branch to interrupt handler
    }
}
```

**How Professor Tests This:**
- "What are the 2 ways CPU can be notified of I/O completion?" (Tutorial 3, Q5)
- MCQ: Polling vs Interrupt — which wastes CPU cycles? Which is more efficient?
- Understanding the interrupt mechanism in the fetch-execute cycle

---

## 3.6 Direct Memory Access (DMA) ⭐⭐⭐

**Core Concept:**
In conventional design, the CPU transfers data between controller data registers and primary memory. For large I/O operations, the CPU gets busy just copying data.

**DMA Solution:**
- DMA controllers can **read/write data from/to memory without CPU intervention**
- DMA controller is like a **mini CPU** — performs the data transfer tasks the CPU would otherwise do
- CPU starts a DMA block transfer, then **performs other work in parallel**
- Significantly increases I/O performance

**What CPU Needs to Provide DMA Controller:**
- Source memory address
- Destination memory address
- Number of bytes to transfer
- Direction of transfer (read/write)

**How Professor Tests This:**
- "What is DMA? What information does CPU need to provide?" (Tutorial 3, Q6)
- MCQ: Why DMA improves performance, what it offloads from CPU

---

# ═══════════════════════════════════════════
# UNIT 4: PROCESS MANAGEMENT
# ═══════════════════════════════════════════

## 4.1 Processes ⭐⭐⭐

**Core Concept:**
A process is a **binary program in execution**. It consists of:
1. A binary program
2. Data on which the program will execute
3. Resources required for execution (files, devices)

**Key Distinction:**
- **Algorithm** → idea
- **Program** → source code → compiled to binary
- **Process** → binary program + data + resources + stack + status = **execution**

**Multiple processes can share the same program** (e.g., multiple users running the same browser), but each has its own data, resources, and stack.

**How Professor Tests This:**
- "What is a process?" (Tutorial 4, Q1)
- MCQ: Difference between a program and a process
- Understanding that a process includes more than just the code

---

## 4.2 Threads ⭐⭐⭐

**Core Concept:**
A thread is a **single execution engine** capable of performing a series of instructions.

| What Threads SHARE | What Threads DON'T SHARE (Thread-specific) |
|-------------------|-------------------------------------------|
| Program code | Program counter |
| Data | Status of the thread |
| Resources (files, devices) | Processor registers |
| | Stack space |

**Why Multithreading?**
1. **Responsiveness** — one thread can continue while another is blocked
2. **Resource sharing** — threads share memory and resources naturally
3. **Ease of memory/resource allocation** — cheaper than creating new processes
4. **Multiprocessor utilization** — threads can run on different CPUs

**Examples:**
- Web browser: one thread displays images, another retrieves data from network
- Word processor: one thread for display, one for keystrokes, one for spell-check

**Single-threaded vs Multi-threaded:**
- Classic process = 1 execution engine (single-threaded)
- Modern process = multiple execution engines (multi-threaded)
- Threads are also called **lightweight processes**

**How Professor Tests This:**
- "In a multi-threaded process, what do threads share and not share? Why?" (Tutorial 4, Q2)
- MCQ: Given a list, identify which are shared vs thread-specific
- Understanding WHY threads share what they share (they're in the same process)

---

## 4.3 Process Manager ⭐⭐

**System Calls for Process Management:**

| Operation | UNIX | Windows |
|-----------|------|---------|
| Create process | `fork()` | `CreateProcess()` |
| Create thread | `pthread_create()` | `CreateThread()` |
| Close process/thread | `close()` | `CloseHandle()` |

**UNIX Process Structure:**
Each process has its own address space subdivided into:
- **Text segment** (code)
- **Data segment** (variables)
- **Stack segment** (function calls, local variables)

**Process Identifier (PID):** User handle for the process descriptor.

**Process Manager Responsibilities:**
1. Define characteristics of processes and threads
2. Define address space
3. Manage resources used by processes/threads
4. Create/destroy/manipulate processes & threads
5. Schedule processes on CPU
6. Allow thread synchronization
7. Handle deadlock
8. Handle protection

---

## 4.4 Process Descriptors (PCB) ⭐⭐⭐

**Core Concept:**
The OS creates a **Process Control Block (PCB)** for each process. This is the data structure that stores all information about a process:

| Field | What It Stores |
|-------|---------------|
| Process ID | Unique identifier |
| Program counter | Address of next instruction |
| Register values | Current register contents |
| Process state | Running/Ready/Blocked/Done |
| Resources held | Type & location of resources |
| Resources needed | List of resources needed |
| Security keys | Access credentials |

PCBs are organized in **queues** (ready queue, wait queues, etc.).

**How Professor Tests This:**
- "What data structure stores process information? How are they organized?" (Tutorial 4, Q4)
- MCQ: What's stored in a PCB

---

## 4.5 Context Switching ⭐⭐⭐

**Core Concept:**
In a multi-process environment, each thread of execution is a **context**. When the CPU switches between two processes/threads, it's a **context switch**.

**Key Points:**
- A context switch can **only occur** when the OS gets control through **traps or interrupts**
- The OS saves the state of the current process (registers, PC) in its PCB
- The OS loads the state of the next process from its PCB
- Context switching has overhead — time spent saving/restoring instead of doing useful work

---

## 4.6 Process States ⭐⭐⭐

**Core Concept:**
As a process executes, it changes state:

| State | Meaning |
|-------|---------|
| **Running** | Instructions being executed |
| **Ready** | Waiting to be assigned to a processor |
| **Blocked** | Waiting for some event (e.g., I/O completion) |
| **Done** | Finished execution |

**State Transition Diagram:**
```
    Start
      ↓
    [Ready] ←─────────────┐
      ↓ ↑                  │
   Schedule/Allocate       │
      ↓ ↑                  │
   [Running]               │
      ↓                    │
   Request I/O/Resource    │
      ↓                    │
   [Blocked] ──────────────┘
      ↓              (I/O complete / Resource allocated)
    [Done]
```

**Windows NT Thread States (more complex):**
- Initialized → Ready → Standby → Running → Waiting → Transition → Terminated
- Additional states support more complex features

**How Professor Tests This:**
- "Given states Running, Ready, Blocked for Interrupt, Blocked for reusable resource, Blocked for consumable resource — draw the state diagram" (Tutorial 4, Q3)
- MCQ: Given a scenario, identify the state transition
- Understanding what triggers each transition

**Tutorial 4 Q3 Answer Framework:**
- Running → Ready: when preempted
- Running → Blocked for Interrupt: waiting for I/O interrupt
- Running → Blocked for Reusable Resource: waiting for memory, files, etc.
- Running → Blocked for Consumable Resource: waiting for messages, signals
- Blocked for Interrupt → Running: interrupt handler finishes
- Blocked for Reusable Resource → Ready: resource allocated
- Blocked for Consumable Resource → Ready: resource produced

---

# ═══════════════════════════════════════════
# UNIT 5: VIRTUAL MEMORY
# ═══════════════════════════════════════════

## 5.1 Virtual Memory Concept ⭐⭐⭐

**Core Concept:**
Sole use of primary memory is insufficient because:
- Large portions of most programs are **not executed most of the time**
- Therefore, those portions need **not be in memory**
- Goal: maximize primary memory use by loading as many programs as possible → increase CPU utilization

**Virtual Memory allows:**
- Execution of processes **not completely in memory**
- Address space partitioned into parts that can be loaded into primary memory
- Parts not needed are written to secondary memory (disk)
- Programs **larger than physical memory** can execute

---

## 5.2 Locality ⭐⭐⭐

**Core Concept:**
Every process has **code and data locality**:
- Code tends to execute in **a few fragments** at one time
- Tends to reference the **same set of data structures**
- As computation moves to a different phase, locality changes

**Example (from slides) — Address Space for program pi:**
| Code Section | Execution Time |
|-------------|---------------|
| Initialization code | Used once |
| Code for Φ1 (phase 1) | 30% |
| Code for Φ2 (phase 2) | 20% |
| Code for Φ3 (phase 3) | 35% |
| Error handling code | <1% |
| Data & stack | 15% |

**Why Locality Works:**
- Process migrates from one locality to another
- Localities may overlap
- Not all code needs to be in memory at once

**Why Thrashing Occurs:**
- Σ size of locality > total memory size

**How Professor Tests This:**
- "Explain code and data locality" (Tutorial 5, Q1)
- MCQ: Why virtual memory works (because of locality)

---

## 5.3 Paging ⭐⭐⭐

**Core Concept:**

| Term | Definition |
|------|-----------|
| **Page** | Fixed-size block of virtual addresses (size = 2^h) |
| **Page Frame** | Fixed-size block of physical memory (same size as a page) |
| **Demand Paging** | Pages are loaded into memory only when needed (not before) |

**Why pages are powers of 2:** Minimizes translation time between virtual and physical addresses.

**Benefits:**
- Programs not constrained by physical memory
- Each program takes less physical memory
- More programs can run simultaneously → higher CPU utilization/throughput

**How Professor Tests This:**
- MCQ: What is a page? What is a page frame?
- Understanding that demand paging is the commercially dominant form today

---

## 5.4 Page Table ⭐⭐⭐

**Core Concept:**
The page table is a **hardware mechanism** that maps:
- **Logical page number** → **Physical page frame number**

**Example:**
```
Logical Memory    Page Table    Physical Memory
Page 0 ─────────→ Frame 2 ─────→ Frame 0
Page 1 ─────────→ Frame 6 ─────→ Frame 1
Page 2 ─────────→ Frame 3 ─────→ Frame 2
Page 3 ─────────→ Frame 7 ─────→ Frame 3
Page 4 ─────────→ Frame 5 ─────→ Frame 4
Page 5 ─────────→ Frame 1 ─────→ Frame 5
                                  Frame 6
                                  Frame 7
```

**Valid-Invalid Bit:**
- Each page table entry has a bit: **1 = in memory (valid)**, **0 = not in memory (invalid)**
- Access to a page marked **invalid** causes a **page-fault trap**
- This distinguishes pages that are in memory from those on disk

**How Professor Tests This:**
- "Given a page table and logical address, find physical address" (Tutorial 5, Q4)
- MCQ: What does the valid-invalid bit do?
- Understanding page fault mechanism

---

## 5.5 Page Fault ⭐⭐⭐

**Core Concept:**
A page fault occurs when a page is required but **not found in primary memory** (it's in virtual memory / on disk).

**Page Replacement Process:**
1. Locate the demand page on disk
2. Find a free frame:
   - If free frame exists → use it
   - Otherwise → use **page replacement algorithm** to select a **victim frame**, write it to disk
3. Read desired page into the newly freed frame
4. Update page and frame tables
5. Restart the user program

**Dirty Bit:** A **modify (dirty) bit** reduces overhead — only modified pages are written to disk (unmodified pages don't need saving).

---

## 5.6 Performance of Demand Paging ⭐⭐⭐

**Effective Access Time (EAT) Formula:**
```
EAT = (1 – p) × memory_access_time + p × (page_fault_overhead + swap_page_out + swap_page_in + restart_overhead)
```

Where:
- p = page fault rate (0 ≤ p ≤ 1)
- p = 0 → no page faults
- p = 1 → every reference is a fault

**Simplified Example (from slides):**
- Memory access time = 1 microsecond
- Page fault service time = 10,000 microseconds (10 ms)
- EAT = (1 – p) × 1 + p × 10,000 = **1 + 9,999p** microseconds

**Key Insight:** EAT is **directly proportional** to page fault rate. Even a tiny page fault rate dramatically increases EAT.

**Tutorial 5 Q2 (Worked Example):**
- Page fault service time = 16 ms = 16,000,000 ns
- Memory access time = 100 ns
- Page fault rate = 0.001
- EAT = (1 – 0.001) × 100 + 0.001 × 16,000,000
- EAT = 0.999 × 100 + 16,000
- EAT = 99.9 + 16,000 = **16,099.9 ns**

---

## 5.7 Thrashing ⭐⭐⭐

**Core Concept:**
If a process doesn't have "enough" pages, the page fault rate is very high. **Thrashing** = a process spends more time paging than executing.

**Symptoms:**
- CPU utilization is low
- OS thinks it needs to increase multiprogramming (which makes it worse!)

**Cause:** Σ size of locality > total memory size

**Solution:** Use a **local (or priority) replacement algorithm** — limits the effects of thrashing.

**How Professor Tests This:**
- "What causes thrashing? How does the system detect it? What can be done?" (Tutorial 5, Q3)
- MCQ: Signs of thrashing, relationship to multiprogramming

---

## 5.8 Tutorial 5 Q4 — Page Table Address Translation (Worked Example) ⭐⭐

Given: Each page is 1024 words.

**For logical address 2056:**
- Page number = 2056 ÷ 1024 = **2** (integer division)
- Offset = 2056 mod 1024 = **8**
- Look up page table for page 2 → find frame number
- Physical address = (frame number, offset)

**For logical address 4500:**
- Page number = 4500 ÷ 1024 = **4** (integer division)
- Offset = 4500 mod 1024 = **404**
- Look up page table for page 4 → if valid, get frame; if invalid → page fault
- Physical address = (frame number, offset)

---

# ═══════════════════════════════════════════
# POWERSHELL SCRIPTING (Part B — 10 Marks)
# ═══════════════════════════════════════════

## P.1 PowerShell Fundamentals ⭐⭐

**Key Concepts:**
- PowerShell is **object-oriented** (not text-based like CMD.EXE)
- Cmdlets are instances of .NET Framework classes (not standalone executables)
- Pipeline passes **objects** (not text streams)
- Parsing, error handling, output formatting handled by PowerShell runtime
- PowerShell is **NOT case sensitive**
- Variable names start with `$`
- Variable types enclosed in `[]`

**Escape Characters (backtick `):**
| Sequence | Meaning |
|----------|---------|
| `` `n `` | New line |
| `` `t `` | Horizontal tab |
| `` `r `` | Carriage return |
| `` `b `` | Backspace |
| `` `a `` | Alert bell |

**Variable Types:**
| Shortcut | Description |
|----------|-------------|
| `[datetime]` | Date or time |
| `[string]` | String of characters |
| `[char]` | Single character |
| `[int]` | 32-bit integer |
| `[double]` | Double-precision floating |
| `[boolean]` | True or False |

**Boolean:** Zero is false, any other number is true.

---

## P.2 Comparison Operators ⭐⭐⭐

**CRITICAL: PowerShell does NOT use ==, <, > for comparisons!**

| Meaning | PowerShell Operator |
|---------|-------------------|
| Equals to | `-eq` |
| Not equal to | `-ne` |
| Greater than | `-gt` |
| Less than | `-lt` |
| Greater than or equal to | `-ge` |
| Less than or equal to | `-le` |
| Pattern matching (wildcards) | `-like` |

---

## P.3 Arithmetic Operators ⭐⭐

| Operator | Description |
|----------|-------------|
| `+`, `+=` | Add |
| `-`, `-=` | Subtract |
| `*`, `*=` | Multiply |
| `/`, `/=` | Divide |
| `%, %=` | Modulus |

---

## P.4 Arrays ⭐⭐⭐

```powershell
# Create an array
$services = @('WinDefend', 'vds', 'Spooler')
$numbers = @(1, 3, 5, 7, 9)

# Access elements
$services[0]    # 'WinDefend'
$services[2]    # 'Spooler'
```

---

## P.5 Loops ⭐⭐⭐

### ForEach Loop
```powershell
$services = @('WinDefend', 'vds', 'Spooler')
foreach ($service in $services) {
    # do something with $service
}
```

### For Loop
```powershell
for ($i = 0; $i -lt 5; $i++) {
    Write-Host $i
}
```

### While Loop
```powershell
while ($condition) {
    # do something
}
```

---

## P.6 If-ElseIf-Else ⭐⭐⭐

```powershell
$status = (Get-Service -Name $service).Status
if ($status -eq 'Running') {
    Write-Host "Service is running" -ForegroundColor Green
}
elseif ($status -eq 'Stopped') {
    Write-Host "Service is stopped" -ForegroundColor Yellow
}
else {
    Write-Host "Service status unknown" -ForegroundColor Red
}
```

---

## P.7 Key Cmdlets ⭐⭐⭐

| Cmdlet | Purpose |
|--------|---------|
| `Get-Service` | Get list of services and their status |
| `Get-Process` | Get list of running processes |
| `Sort-Object` / `Sort` | Sort objects by property |
| `Select-Object` | Select specific properties |
| `Write-Host` | Display output with color options |
| `Write-Output` / `echo` | Output objects to pipeline |
| `Where-Object` | Filter objects |
| `Get-Member` | List methods and properties of objects |
| `Get-ChildItem` | Get items in a location |
| `Read-Host` | Read input from console |
| `Get-ExecutionPolicy` | Check script execution policy |
| `Set-ExecutionPolicy` | Set script execution policy |

---

## P.8 Redirection Operators ⭐⭐⭐

| Operator | What It Does | File Already Has Data? |
|----------|-------------|----------------------|
| `>` | Writes output to file | **Overwrites** (replaces) existing content |
| `>>` | Appends output to file | **Appends** to existing content |

**How Professor Tests This:**
- "Explain the difference between > and >>" (Revision Q1)
- MCQ: What happens to existing file content with each operator

---

## P.9 The Pipeline ⭐⭐⭐

**Core Concept:**
The pipeline operator `|` passes the **output object** of one command as **input** to the next command.

```powershell
Get-Process | Sort-Object -Property ID
```

This retrieves all processes, then pipes the **objects** (not text) to Sort-Object, which sorts by the ID property.

**How Professor Tests This:**
- "Describe what happens to data when passed through the pipeline" (Revision Q2)
- MCQ: Given a pipeline, predict the output

---

## P.10 Error Handling with Get-Service ⭐⭐

**Problem:** Querying a non-existent service results in an error.

**Solution:** Use the `-ErrorAction SilentlyContinue` parameter to suppress the error, allowing If-Else to gracefully handle "missing" items.

```powershell
$service = Get-Service -Name "NonExistent" -ErrorAction SilentlyContinue
if ($service) {
    # service exists
} else {
    # service not found
}
```

---

## P.11 Useful Cmdlets from Exam Help Sheet ⭐⭐

**Get-Service:**
```
Get-Service [[-Name] <String[]>] [-DependentServices] [-RequiredServices] [-Include <String[]>] [-Exclude <String[]>]
```

**Get-Process:**
```
Get-Process [[-Name] <String[]>] [-Module] [-FileVersionInfo]
```

**Sort-Object:**
```
Sort-Object [[-Property] <Object[]>] [-Stable] [-Descending] [-Unique] [-InputObject <PSObject>]
```

**Write-Host:**
```
Write-Host [[-Object] <Object>] [-NoNewline] [-ForegroundColor <ConsoleColor>] [-BackgroundColor <ConsoleColor>]
```

---

# ═══════════════════════════════════════════
# QUICK-FIRE MCQ REVISION
# ═══════════════════════════════════════════

1. **Q:** What role does the OS play from the user's perspective?
   **A:** Intermediary between user and hardware; provides environment for program execution.

2. **Q:** Name 3 components of system software.
   **A:** OS, compiler, window system, DBMS, libraries, loader (any 3).

3. **Q:** Can you use a computer without an OS?
   **A:** No — you need an OS to load and execute programs, manage hardware.

4. **Q:** A personal computer — space or time multiplexed?
   **A:** Time multiplexed (one user at a time uses the entire resource).

5. **Q:** A printer on a timesharing system — space or time multiplexed?
   **A:** Time multiplexed (each job gets the printer for its turn).

6. **Q:** What does abstraction hide?
   **A:** The actual tasks needed to manage and use resources.

7. **Q:** In which mode does the kernel execute?
   **A:** Supervisor mode — it needs access to all instructions and memory.

8. **Q:** Why are I/O instructions privileged?
   **A:** They directly control hardware; if user programs could execute them, they could bypass security and interfere with other processes.

9. **Q:** What is more efficient — system call or message passing?
   **A:** System call (just needs a trap instruction; message passing has message formation/copying overhead).

10. **Q:** What does the trap instruction do?
    **A:** Switches from user mode to supervisor mode, entering the OS via the trap table.

11. **Q:** What architecture is the modern computer based on?
    **A:** Von Neumann architecture — CPU (ALU + CU), primary memory, I/O devices, buses.

12. **Q:** What algorithm does the control unit follow?
    **A:** Fetch-execute cycle — fetch instruction from memory (PC), load into IR, execute, increment PC.

13. **Q:** What are the 3 registers for CPU-memory interaction?
    **A:** MAR (address), MDR (data), CMD (command).

14. **Q:** Polling vs Interrupt — which wastes CPU cycles?
    **A:** Polling — CPU busy-waits checking device status.

15. **Q:** What does DMA allow?
    **A:** Device controller to read/write memory without CPU intervention.

16. **Q:** What is a process?
    **A:** A binary program in execution (program + data + resources + stack + status).

17. **Q:** What do threads in the same process share?
    **A:** Program code, data, resources. They DON'T share: PC, registers, stack, status.

18. **Q:** When can a context switch occur?
    **A:** Only when the OS gets control through traps or interrupts.

19. **Q:** What are the basic process states?
    **A:** Running, Ready, Blocked, Done.

20. **Q:** What causes thrashing?
    **A:** Process doesn't have enough pages; Σ locality size > total memory size.

21. **Q:** What is a page fault?
    **A:** Event when a required page is not in primary memory but is in virtual memory (on disk).

22. **Q:** What does the valid-invalid bit do?
    **A:** Distinguishes pages in memory (valid=1) from pages on disk (invalid=0). Invalid access causes page fault.

23. **Q:** What is demand paging?
    **A:** Pages are loaded into memory only when needed, not before.

24. **Q:** PowerShell: What is the equals comparison operator?
    **A:** `-eq` (NOT `==`).

25. **Q:** PowerShell: What does `>` do to an existing file?
    **A:** Overwrites the entire file.

26. **Q:** PowerShell: What does `>>` do?
    **A:** Appends to the file.

27. **Q:** PowerShell: What does the pipeline `|` pass?
    **A:** Objects (not text) from one command to the next.

28. **Q:** What parameter suppresses errors in Get-Service?
    **A:** `-ErrorAction SilentlyContinue`

29. **Q:** Monolithic vs Microkernel — which combines all modules?
    **A:** Monolithic (e.g., UNIX). Microkernel keeps only essential functions in kernel.

30. **Q:** What is the PCB?
    **A:** Process Control Block — data structure storing all process information (PID, PC, registers, state, resources).

---

# ═══════════════════════════════════════════
# CROSS-TOPIC CONNECTIONS
# ═══════════════════════════════════════════

These are the connections the professor loves to test:

1. **Abstraction (Ch1) → Process/Memory/File/Device Managers (Ch2)** — Each manager creates abstractions for its resource type.

2. **Resource Sharing (Ch1) → Processor Modes (Ch2)** — Supervisor/User modes enable the OS to control how resources are shared.

3. **Multiprogramming (Ch1) → Context Switching (Ch4) → Virtual Memory (Ch5)** — Multiprogramming needs context switching, which needs virtual memory to work efficiently.

4. **Polling/Interrupt (Ch3) → Process States (Ch4)** — A process waiting for I/O is in Blocked state; interrupt moves it to Ready.

5. **DMA (Ch3) → Device Management (Ch2)** — DMA is a device management optimization that frees the CPU.

6. **Locality (Ch5) → Demand Paging (Ch5) → Multiprogramming (Ch1)** — Locality principle makes demand paging work, which enables more programs in memory.

7. **System Calls (Ch2) → Process Management (Ch4)** — fork(), CreateProcess() are system calls that cross from user to supervisor mode.

8. **Pipeline (PowerShell) → Abstraction (Ch1)** — PowerShell pipeline abstracts away the details of passing data between commands.
