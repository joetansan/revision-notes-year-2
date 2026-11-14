# IT2515 Practice Problems — With Hidden Solutions
### Chapters 1–5 + PowerShell | Self-Test Edition

> **How to use:** Attempt each problem BEFORE clicking the solution. Mark yourself honestly.
> - MCQs: 1 mark each
> - Short answer: 2–4 marks each
> - Numerical: 3–4 marks each
> - PowerShell: as marked

---

# ═══════════════════════════════════════════
# CHAPTER 1: INTRODUCTION TO OPERATING SYSTEMS
# ═══════════════════════════════════════════

### Problem 1.1 — OS Role ⭐
From the user's point of view, what role does the operating system play in the overall functioning of the computer?

<details>
<summary>🔓 Click to reveal solution</summary>

The OS acts as an **intermediary** between the user and the computer hardware. It provides an environment in which users can execute programs in a convenient and efficient manner. It manages hardware resources on behalf of the user so they don't need to deal with raw hardware operations.

</details>

---

### Problem 1.2 — System Software Components ⭐
List any 3 components of the system software of a computer system.

<details>
<summary>🔓 Click to reveal solution</summary>

Any three of:
- Operating System
- Compiler
- Window System
- Database Management System (DBMS)
- Libraries (e.g., C library functions)
- Resource management functions
- Loader
- Command Line Interpreter

</details>

---

### Problem 1.3 — OS Necessity ⭐
Is it possible for a person to buy a computer and use it without an operating system? Why?

<details>
<summary>🔓 Click to reveal solution</summary>

**No.** Without an OS, there is no program to load and execute other programs, manage hardware resources, or provide a user interface. The OS is the intermediary that makes the hardware usable. Application programs depend on the OS to access hardware, manage memory, and handle I/O. Without it, the computer is just a collection of electronic parts with no way to coordinate them.

</details>

---

### Problem 1.4 — Space vs Time Multiplexing ⭐⭐
Identify which of the following are examples of space-multiplexed sharing, and which are time-multiplexed sharing. If there is a sense that it could be either strategy, explain.

a. The land in a residential zone
b. A personal computer
c. A whiteboard in a classroom
d. A bench seat on a bus
e. A single-user file in the computer
f. A printer on a timesharing system

<details>
<summary>🔓 Click to reveal solution</summary>

| Item | Type | Explanation |
|------|------|-------------|
| a. Land in residential zone | **Space-multiplexed** | Each house gets its own plot of land |
| b. Personal computer | **Time-multiplexed** | One user at a time uses the entire machine |
| c. Whiteboard in classroom | **Either** | Space: divide into sections for different groups. Time: erase between uses, different people use at different times |
| d. Bench seat on bus | **Space-multiplexed** | Each passenger sits in a distinct section of the bench |
| e. Single-user file | **Time-multiplexed** | One user accesses the file at a time |
| f. Printer on timesharing | **Time-multiplexed** | Each print job takes turns using the entire printer |

</details>

---

### Problem 1.5 — Multiprogramming Factors ⭐⭐
Discuss some factors that must be considered in determining the maximum number of multiprogrammed processes for a particular system. You may assume a batch system with the same number of processes as jobs.

<details>
<summary>🔓 Click to reveal solution</summary>

Key factors include:
- **Available memory** — each process needs memory; more processes = less memory per process
- **CPU speed vs I/O speed** — if I/O is the bottleneck, more processes can keep CPU busy
- **Number and speed of I/O devices** — more devices means more processes can do I/O simultaneously
- **Process characteristics** — how much CPU vs I/O each process needs
- **Overhead of context switching** — too many processes means too much time spent switching
- **Disk speed** — affects swap time if virtual memory is used
- **Resource availability** — files, devices, and other resources each process needs

</details>

---

### Problem 1.6 — Batch vs Timesharing ⭐⭐
When is batch processing the preferred strategy for work to be done by the computer? When is timesharing the preferred strategy?

<details>
<summary>🔓 Click to reveal solution</summary>

**Batch processing is preferred when:**
- Jobs can be prepared offline
- No human-computer interaction is needed during execution
- Throughput (jobs completed per unit time) is more important than response time
- Examples: payroll processing, end-of-day reports, scientific simulations

**Timesharing is preferred when:**
- Interactive computing is needed
- Multiple users need simultaneous access
- Response time is critical
- Users need to interact with running programs
- Examples: university computing systems, multi-user servers

</details>

---

### Problem 1.7 — MCQ: Resource Abstraction ⭐
Which statement best describes resource abstraction?

A) The OS allows multiple users to share the same hardware
B) The OS hides the actual tasks needed to manage and use resources, providing simpler commands
C) The OS allocates CPU time to each process equally
D) The OS converts high-level programming languages to machine code

<details>
<summary>🔓 Click to reveal solution</summary>

**B)** The OS hides the actual tasks needed to manage and use resources, providing simpler commands.

Abstraction simplifies usage but limits flexibility — certain operations become easy while others may become impossible. Example: `fprintf()` abstracts away the low-level disk operations that `write()` and `load()/seek()/out()` handle.

</details>

---

### Problem 1.8 — MCQ: Multiprogramming ⭐
What is the primary benefit of multiprogramming?

A) It makes programs run faster
B) It increases CPU utilization by allowing another process to run while one is blocked
C) It reduces the amount of memory needed
D) It eliminates the need for an operating system

<details>
<summary>🔓 Click to reveal solution</summary>

**B)** It increases CPU utilization by allowing another process to run while one is blocked.

When one process is waiting for I/O or another resource, the CPU can execute a different process. This keeps the CPU busy and increases overall utilization.

</details>

---

# ═══════════════════════════════════════════
# CHAPTER 2: OPERATING SYSTEM ORGANIZATION
# ═══════════════════════════════════════════

### Problem 2.1 — Abstraction Explanation ⭐⭐
Briefly explain abstraction in terms of an OS managing the resources of a computer system.

<details>
<summary>🔓 Click to reveal solution</summary>

Abstraction is when the OS hides the actual tasks needed to manage and use resources. It allows user programs to use resources by using simpler commands instead of dealing with hardware directly. For example, writing a file to disk involves complex low-level operations (load, seek, out), but the OS abstracts these into a simple `fprintf()` call. This makes it easy for programs to use resources but limits flexibility — some low-level operations become impossible to perform directly.

</details>

---

### Problem 2.2 — Kernel Execution Mode ⭐⭐
In which mode does the kernel execute in the processor? Why is it so?

<details>
<summary>🔓 Click to reveal solution</summary>

The kernel executes in **supervisor mode**. This is because the kernel is the trusted part of the OS critical to correct operation. It needs to:
- Execute **all** machine instructions, including privileged instructions (I/O, memory-related, mode-change)
- Access **all** memory locations, including system/supervisor space
- Control access to resources and maintain system security

Only supervisor mode provides these capabilities. User mode restricts instructions and memory access, which would prevent the kernel from performing its essential functions.

</details>

---

### Problem 2.3 — System Call vs Procedure Call ⭐⭐
What are some of the factors that differentiate between the time to do a normal procedure call from an application program to one of its own procedures, compared to the time it takes to perform a system call to an OS procedure?

<details>
<summary>🔓 Click to reveal solution</summary>

Factors that make system calls slower than normal procedure calls:
- **Mode switch**: System call requires switching from user mode to supervisor mode (and back), which has overhead
- **Trap instruction execution**: The trap instruction must be executed, which branches to the trap table
- **Trap table lookup**: The system must look up the entry point of the OS function in the trap table
- **Parameter validation**: The OS must verify that the user program's parameters are valid and safe
- **Context saving**: The system must save the user process state before executing the kernel code
- **Return overhead**: Switching back to user mode and restoring the user process state

A normal procedure call just requires a simple branch-and-link within the same mode and address space.

</details>

---

### Problem 2.4 — UNIX Monolithic Kernel ⭐⭐
Suggest some reasons why UNIX is a monolithic kernel.

<details>
<summary>🔓 Click to reveal solution</summary>

Reasons UNIX uses a monolithic kernel:
- **Performance**: All four managers (process, memory, file, device) in a single module means no inter-module communication overhead — direct function calls instead of message passing
- **Simplicity of design**: Single module is easier to optimize as a whole
- **Historical context**: Developed in 1970 when hardware was limited; minimizing overhead was critical
- **Tight integration**: Process, memory, file, and device management need to interact frequently; putting them in one module makes these interactions faster
- **Efficiency**: Avoids the cost of crossing module boundaries for frequent operations

The trade-off is reduced modularity, but for UNIX's use case (timesharing system), performance was prioritized.

</details>

---

### Problem 2.5 — Privileged Instructions ⭐⭐
Explain why I/O and memory instructions are privileged instructions.

<details>
<summary>🔓 Click to reveal solution</summary>

I/O and memory instructions are privileged because they directly control hardware resources:

**I/O instructions** are privileged because:
- They control external devices (disk, printer, network)
- If user programs could execute them directly, they could read/write any device, bypass security
- Could interfere with other processes' I/O operations
- Could corrupt data on storage devices

**Memory instructions** are privileged because:
- They control what memory locations can be accessed
- If user programs could execute them, they could access or modify other processes' memory
- Could bypass memory isolation and protection
- Could corrupt the OS kernel's memory, causing system crashes

Making these privileged forces user programs to request these operations through the OS, which can enforce access control and protection policies.

</details>

---

### Problem 2.6 — MCQ: Four OS Managers ⭐
Which of the following is NOT one of the four major OS managers?

A) Process, Thread and Resource Manager
B) Network Manager
C) Memory Manager
D) File Manager

<details>
<summary>🔓 Click to reveal solution</summary>

**B) Network Manager**

The four major managers are:
1. Process, Thread and Resource Manager
2. Memory Manager
3. Device Manager
4. File Manager

</details>

---

### Problem 2.7 — MCQ: System Call Mechanism ⭐
In a system call, what instruction is used to switch from user mode to supervisor mode?

A) Interrupt instruction
B) Jump instruction
C) Trap instruction
D) Branch instruction

<details>
<summary>🔓 Click to reveal solution</summary>

**C) Trap instruction**

The trap instruction switches the processor from user mode to supervisor mode and branches to the trap table, which contains the entry points of OS system functions. The stub function provided by the OS executes this trap instruction on behalf of the user program.

</details>

---

### Problem 2.8 — MCQ: Supervisor vs User Mode ⭐
Which of the following can a processor in user mode do?

A) Execute all machine instructions including privileged instructions
B) Access all memory locations including system space
C) Execute only non-privileged instructions and access only user space
D) Switch between supervisor and user mode freely

<details>
<summary>🔓 Click to reveal solution</summary>

**C)** Execute only non-privileged instructions and access only user space.

User mode restricts programs to a subset of instructions and memory. To perform privileged operations, user programs must make system calls that switch to supervisor mode.

</details>

---

# ═══════════════════════════════════════════
# CHAPTER 3: COMPUTER ORGANIZATION
# ═══════════════════════════════════════════

### Problem 3.1 — Von Neumann Architecture ⭐⭐
What architecture is the modern computer based on? Briefly describe the architecture.

<details>
<summary>🔓 Click to reveal solution</summary>

Modern computers are based on the **von Neumann architecture**. It consists of:

1. **CPU (Central Processing Unit)** — contains:
   - ALU (Arithmetical-Logical Unit) — performs arithmetic and logical operations
   - Control Unit — fetches, decodes, and executes instructions using the fetch-execute cycle

2. **Primary Memory Unit** — stores both programs and data while being operated on by the CPU (RAM)

3. **I/O Devices** — for input, output, communications, and storage

4. **Buses** — interconnect the components:
   - Address Bus — carries memory addresses
   - Data Bus — carries data

The key concept is the **stored program** — a fixed set of electronic parts can be manipulated to perform various tasks determined by a variable program stored in memory.

</details>

---

### Problem 3.2 — Control Unit Algorithm ⭐⭐
What algorithm does the control unit follow? Briefly describe the algorithm.

<details>
<summary>🔓 Click to reveal solution</summary>

The control unit follows the **fetch-execute cycle**:

1. **Fetch phase:**
   - Retrieve instruction from memory at the address specified by the **Program Counter (PC)**
   - Load the instruction into the **Instruction Register (IR)**
   - Increment the PC to point to the next instruction

2. **Execute phase:**
   - Decode the instruction in the IR
   - Signal the ALU to execute the operation
   - May cause memory data reference, I/O operation, or other actions

This cycle repeats continuously from when the computer is powered up until it is shut down.

```
PC = machine start address
IR = memory[PC]
while (haltFlag not set) {
    execute(IR)
    PC = PC + sizeof(INSTRUCTION)
    IR = memory[PC]
}
```

</details>

---

### Problem 3.3 — CPU-Memory Registers ⭐⭐
What are the 3 main registers that are used by the CPU to interact with the main memory?

<details>
<summary>🔓 Click to reveal solution</summary>

| Register | Full Name | Purpose |
|----------|-----------|---------|
| **MAR** | Memory Address Register | Stores the address of data to be read from or written to memory |
| **MDR** | Memory Data Register | Stores the data that is read from memory or is to be written to memory |
| **CMD** | Command Register | Stores the command to be executed (e.g., "read" or "write") |

</details>

---

### Problem 3.4 — CPU-I/O Overlap ⭐⭐
Why do we want to have the CPU's operation overlap with that of the I/O processing?

<details>
<summary>🔓 Click to reveal solution</summary>

Devices are much slower than the CPU. If the CPU waits for I/O to complete, it wastes precious processor cycles doing nothing. By overlapping CPU and I/O operations:

- While Process A is waiting for I/O, the CPU can execute Process B
- This is the fundamental principle behind **multiprogramming**
- It increases **CPU utilization** and overall system throughput
- The CPU doesn't sit idle while slow devices (disk, printer, network) do their work

This overlap is what makes multiprogramming possible — without it, the CPU would be idle during every I/O operation.

</details>

---

### Problem 3.5 — I/O Completion Methods ⭐⭐
What are the 2 ways in which the CPU can be notified of the completion of an I/O operation?

<details>
<summary>🔓 Click to reveal solution</summary>

**1. Polling:**
- CPU continuously checks (polls) the device status flag
- If I/O not done, CPU executes a busy-wait loop
- Simple but **wastes CPU cycles** — CPU is effectively doing nothing while waiting

**2. Interrupt:**
- CPU has an "interrupt pending" flag
- When device finishes, it sets the interrupt flag
- CPU detects the flag during its fetch-execute cycle
- CPU branches to an interrupt handler routine
- **More efficient** — CPU can do other work while waiting for I/O

</details>

---

### Problem 3.6 — DMA ⭐⭐⭐
What is DMA? What information do you think the CPU needs to provide the DMA controller to issue a memory transfer operation?

<details>
<summary>🔓 Click to reveal solution</summary>

**DMA (Direct Memory Access)** is a mechanism where the DMA controller can read/write data from/to primary memory **without CPU intervention**. The DMA controller acts like a mini CPU, performing data transfer tasks that the CPU would otherwise have to do. This allows the CPU to perform other work in parallel with the DMA operation, significantly increasing I/O performance.

**Information the CPU must provide the DMA controller:**
1. **Source address** — where to read data from (memory address or device register)
2. **Destination address** — where to write data to (memory address or device register)
3. **Transfer size** — number of bytes/words to transfer
4. **Direction** — read from device to memory, or write from memory to device
5. **Device identification** — which device is involved in the transfer

</details>

---

### Problem 3.7 — MCQ: Fetch-Execute Cycle ⭐
During the fetch phase of the fetch-execute cycle, what happens to the Program Counter (PC)?

A) It is reset to zero
B) It is decremented by one
C) It is incremented to point to the next instruction
D) It stores the result of the current instruction

<details>
<summary>🔓 Click to reveal solution</summary>

**C)** It is incremented to point to the next instruction.

During the fetch phase: instruction is retrieved from memory at the address in PC → loaded into IR → PC is incremented. This ensures the next iteration fetches the following instruction.

</details>

---

### Problem 3.8 — MCQ: Device Controller Status ⭐
A device controller has status flags busy=0 and done=1. What is the device state?

A) Idle
B) Working
C) Finished
D) Undefined

<details>
<summary>🔓 Click to reveal solution</summary>

**C) Finished**

| busy | done | State |
|------|------|-------|
| 0 | 0 | Idle |
| 0 | 1 | Finished |
| 1 | 0 | Working |
| 1 | 1 | Undefined |

</details>

---

# ═══════════════════════════════════════════
# CHAPTER 4: PROCESS MANAGEMENT
# ═══════════════════════════════════════════

### Problem 4.1 — What is a Process? ⭐⭐
What is a process?

<details>
<summary>🔗 Click to reveal solution</summary>

A process is a **binary program in execution**. It consists of:
1. A **binary program** (compiled code)
2. **Data** on which the program will execute
3. **Resources** required for execution (files, devices)
4. A **stack** (for function calls, local variables)
5. **Status** information (current state of execution)

Key distinction: A program is a static file on disk. A process is a dynamic entity — the same program can have multiple processes running simultaneously, each with its own data, resources, and stack.

</details>

---

### Problem 4.2 — Thread Sharing ⭐⭐⭐
In a multi-threaded process, threads share certain information in the same process whilst not sharing others. In your own words, briefly explain why this is so.

<details>
<summary>🔓 Click to reveal solution</summary>

**Threads SHARE** (because they belong to the same process):
- **Program code** — they execute the same program
- **Data** — they operate on the same data/variables
- **Resources** — they have access to the same files, devices

**Threads DON'T SHARE** (because each is an independent execution engine):
- **Program counter** — each thread is at a different point in the code
- **Processor registers** — each thread has its own computation state
- **Stack** — each thread has its own function call history and local variables
- **Status** — each thread can be in a different state (one running, one blocked)

**Why:** The shared items define WHAT the process does (code, data, resources). The non-shared items define WHERE each thread is in that execution (its current position, local state). Multiple threads can be executing different parts of the same program simultaneously, so each needs its own execution context.

</details>

---

### Problem 4.3 — Process State Diagram ⭐⭐⭐
Given that the states of a process are:
- Running: Currently using the CPU
- Ready: Waiting for the CPU
- Blocked for Interrupt: Waiting for an interrupt handler to finish, then resume running
- Blocked for reusable resource: Waiting for a reusable resource to be allocated, then will become ready
- Blocked for consumable resource: Waiting for a consumable resource to be allocated, then will become ready

What is a possible state diagram for the process? Show the relationship in terms of the transitions between each of these states.

<details>
<summary>🔓 Click to reveal solution</summary>

```
                    ┌─────────────────────────────┐
                    │                             │
                    ▼                             │
                ┌───────┐    Schedule/      ┌──────────┐
     Start ───►│ Ready │    Dispatch       │ Running  │
                └───────┘◄─────────────────└──────────┘
                    ▲                      │    │    │
                    │                      │    │    │
        Resource    │                      │    │    │
        allocated   │              Preempt │    │    │
                    │                      │    │    │
                    │                      ▼    │    │
                    │              ┌──────────┐  │    │
                    ├──────────────│ Blocked  │  │    │
                    │              │ for      │  │    │
                    │              │ Reusable │  │    │
                    │              │ Resource │  │    │
                    │              └──────────┘  │    │
                    │                            │    │
                    │              Request       │    │
                    │              resource      │    │
                    │                            │    │
                    │              ┌──────────┐  │    │
                    ├──────────────│ Blocked  │  │    │
                    │              │ for      │  │    │
                    │              │ Consum-  │  │    │
                    │              │ able     │  │    │
                    │              │ Resource │  │    │
                    │              └──────────┘  │    │
                    │                            │    │
                    │              ┌──────────┐  │    │
                    └──────────────│ Blocked  │◄─┘    │
                                   │ for      │       │
                                   │ Interrupt│       │
                                   └──────────┘       │
                                        │             │
                                        │ Interrupt   │
                                        │ complete    │
                                        └─────────────┘
                                        (returns to Running)
```

**Transitions:**
- **Start → Ready**: Process is created
- **Ready → Running**: Scheduler dispatches process to CPU
- **Running → Ready**: Process is preempted (time slice expires)
- **Running → Blocked for Interrupt**: Process initiates I/O, waits for interrupt
- **Running → Blocked for Reusable Resource**: Process requests reusable resource (memory, file)
- **Running → Blocked for Consumable Resource**: Process requests consumable resource (message, signal)
- **Blocked for Interrupt → Running**: Interrupt handler completes, process resumes execution
- **Blocked for Reusable Resource → Ready**: Resource is allocated
- **Blocked for Consumable Resource → Ready**: Resource is produced/available

</details>

---

### Problem 4.4 — PCB Data Structure ⭐⭐
What data structure is used to store the information regarding each process in the OS? How are they organized?

<details>
<summary>🔓 Click to reveal solution</summary>

The **Process Control Block (PCB)** (also called process descriptor) is used to store all information about each process.

**Contents of a PCB:**
- Process ID (PID)
- Program counter (address of next instruction)
- Register values
- Process state (Running/Ready/Blocked/Done)
- Type and location of resources held
- List of resources needed
- Security keys
- Memory management information (page table, memory limits)

**Organization:** PCBs are organized in **queues**:
- Ready queue — PCBs of processes in Ready state
- Wait queues — PCBs of processes waiting for specific events/resources
- Each queue is typically a linked list of PCBs

</details>

---

### Problem 4.5 — MCQ: Process vs Program ⭐
What is the difference between a program and a process?

A) A program is in memory, a process is on disk
B) A program is static code on disk, a process is a program in execution with data, resources, and state
C) A process is written in high-level language, a program is in machine code
D) There is no difference

<details>
<summary>🔓 Click to reveal solution</summary>

**B)** A program is static code on disk, a process is a program in execution with data, resources, and state.

A program is a file of instructions. A process includes the binary program + data + resources + stack + status. Multiple processes can share the same program (e.g., multiple browser windows).

</details>

---

### Problem 4.6 — MCQ: Context Switching ⭐
When can a context switch occur?

A) At any time during program execution
B) Only when the user presses Ctrl+C
C) Only when the OS gets control through traps or interrupts
D) Only when a process terminates

<details>
<summary>🔓 Click to reveal solution</summary>

**C)** Only when the OS gets control through traps or interrupts.

A context switch requires the OS to save the current process state and load another process's state. This can only happen when the OS has control of the CPU, which occurs through:
- **Traps** — system calls, errors
- **Interrupts** — I/O completion, timer

User programs cannot voluntarily switch contexts — they must go through the OS.

</details>

---

### Problem 4.7 — MCQ: Benefits of Multithreading ⭐
Which of the following is NOT a benefit of multithreaded programming?

A) Responsiveness
B) Resource sharing
C) Elimination of context switching overhead
D) Utilization of multiprocessor architectures

<details>
<summary>🔓 Click to reveal solution</summary>

**C)** Elimination of context switching overhead.

Multithreading actually still involves context switching between threads. The benefits are:
- Responsiveness (one thread can continue while another is blocked)
- Resource sharing (threads share memory naturally)
- Ease of memory and resource allocation
- Utilization of multiprocessors (threads can run on different CPUs)

</details>

---

# ═══════════════════════════════════════════
# CHAPTER 5: VIRTUAL MEMORY
# ═══════════════════════════════════════════

### Problem 5.1 — Code and Data Locality ⭐⭐
In your own words, explain what is meant by code and data locality?

<details>
<summary>🔓 Click to reveal solution</summary>

**Code locality** means that a program tends to execute only a small portion of its code at any given time. For example, during initialization, only the initialization code runs. During the main processing phase, only that specific code runs. The program doesn't jump randomly between all its code — it stays in a "locality" of related code.

**Data locality** means that a program tends to reference the same set of data structures repeatedly during a given phase of execution. It doesn't randomly access all data in memory — it works with a consistent set of variables and data.

**Why it matters:** This principle is what makes virtual memory work. Since only a small portion of code and data is actively used, only those portions need to be in physical memory at any time. The rest can stay on disk.

**Phase changes:** As computation moves to a different phase (e.g., from initialization to main processing), the locality changes — different code and data become active.

</details>

---

### Problem 5.2 — Effective Access Time Calculation ⭐⭐⭐
Assume we have a demand-paged memory. The page table is held in registers. It takes 16 milliseconds to service a page fault. Memory access time is 100 nanoseconds. Assume that page-fault rate is 0.001. What is the effective access time for this memory system? (Note: 1 millisecond = 1,000 microseconds = 1,000,000 nanoseconds)

<details>
<summary>🔓 Click to reveal solution</summary>

**Given:**
- Page fault service time = 16 ms = 16,000,000 ns
- Memory access time = 100 ns
- Page fault rate (p) = 0.001

**Formula:**
```
EAT = (1 – p) × memory_access_time + p × page_fault_service_time
```

**Calculation:**
```
EAT = (1 – 0.001) × 100 + 0.001 × 16,000,000
EAT = 0.999 × 100 + 16,000
EAT = 99.9 + 16,000
EAT = 16,099.9 nanoseconds
```

**Answer: EAT = 16,099.9 ns ≈ 16.1 microseconds**

**Key insight:** Even with a very low page fault rate (0.1%), the EAT is 161× slower than the base memory access time. This shows how expensive page faults are.

</details>

---

### Problem 5.3 — Thrashing ⭐⭐⭐
What is the cause of thrashing? How does the system detect thrashing? Once it detects thrashing, what can the system do to eliminate this problem?

<details>
<summary>🔓 Click to reveal solution</summary>

**Cause of thrashing:**
A process does not have "enough" page frames allocated to it. When the sum of all active localities exceeds total available memory, each process constantly page-faults trying to bring in its needed pages, evicting pages that other processes need.

**How the system detects thrashing:**
- CPU utilization drops significantly (processes spend more time paging than executing)
- Page fault rate increases dramatically
- The OS may initially think it needs to increase multiprogramming (adding more processes), which actually makes thrashing worse

**How to eliminate thrashing:**
- Use a **local (or priority) replacement algorithm** — each process only replaces its own pages, preventing one process from stealing pages from another
- Reduce the degree of multiprogramming (remove some processes)
- Allocate sufficient page frames to each process based on its working set size

</details>

---

### Problem 5.4 — Page Table Address Translation ⭐⭐⭐
Given the following demand paging system, fill in the entries in the page table by writing the appropriate frame number. Enter i or v in the valid/invalid bit. Assuming that each page is 1024 words, write the physical address of the following logical address of the process, in the form (page frame no, offset) format:
(i) 2056
(ii) 4500

*(Reference: See Tutorial 5 diagram for the page table and memory layout)*

<details>
<summary>🔓 Click to reveal solution</summary>

**Step 1: Determine page number and offset for each logical address**

For logical address **2056**:
- Page number = 2056 ÷ 1024 = **2** (integer division)
- Offset = 2056 mod 1024 = 2056 - (2 × 1024) = 2056 - 2048 = **8**

For logical address **4500**:
- Page number = 4500 ÷ 1024 = **4** (integer division)
- Offset = 4500 mod 1024 = 4500 - (4 × 1024) = 4500 - 4096 = **404**

**Step 2: Look up page table**

Based on the Tutorial 5 diagram:
- Page 0 → Frame C (valid)
- Page 1 → not in memory (invalid)
- Page 2 → Frame A (valid)
- Page 3 → Frame D (valid)
- Page 4 → not in memory (invalid) → **page fault!**
- Page 5 → Frame E (valid)

**Step 3: Physical addresses**

(i) Logical address 2056 → Page 2, Offset 8 → Frame A → **Physical address: (A, 8)**

(ii) Logical address 4500 → Page 4, Offset 404 → **Page fault!** Page 4 is not in memory (invalid bit = i). The system must bring the page from disk into a free frame before the address can be translated.

**General method:**
1. Page number = logical address ÷ page size (integer division)
2. Offset = logical address mod page size
3. Look up page table: if valid, get frame number; if invalid, page fault
4. Physical address = (frame number, offset)

</details>

---

### Problem 5.5 — MCQ: Demand Paging ⭐
What is demand paging?

A) All pages of a process are loaded into memory before execution begins
B) Pages are loaded into memory only when they are needed during execution
C) Pages are loaded into memory in alphabetical order
D) Pages are loaded into memory based on priority

<details>
<summary>🔓 Click to reveal solution</summary>

**B)** Pages are loaded into memory only when they are needed during execution.

In pure demand paging, the system never brings a page into memory until it is needed. This avoids reading pages that will never be used, decreasing swap time and the amount of physical memory needed per process.

</details>

---

### Problem 5.6 — MCQ: Page Fault ⭐
What happens when a process accesses a page marked as invalid in the page table?

A) The process terminates immediately
B) The page is automatically loaded from disk
C) A page-fault trap occurs, and the OS must handle bringing the page into memory
D) The access is silently ignored

<details>
<summary>🔓 Click to reveal solution</summary>

**C)** A page-fault trap occurs, and the OS must handle bringing the page into memory.

The valid-invalid bit scheme distinguishes pages in memory (valid=1) from pages on disk (invalid=0). Access to an invalid page triggers a trap to the OS, which must locate the page on disk, find a free frame (or replace a victim frame), read the page in, update the page table, and restart the instruction.

</details>

---

### Problem 5.7 — MCQ: Dirty Bit ⭐
What is the purpose of the dirty (modify) bit in page replacement?

A) To mark pages that contain errors
B) To indicate pages that have been modified, so only those pages need to be written back to disk
C) To mark pages that are corrupted
D) To indicate pages that should never be replaced

<details>
<summary>🔓 Click to reveal solution</summary>

**B)** To indicate pages that have been modified, so only those pages need to be written back to disk.

When replacing a page, if the page was not modified (dirty bit = 0), there's no need to write it back to disk since the disk copy is already up to date. Only modified pages (dirty bit = 1) need to be written back. This reduces the overhead of page transfers.

</details>

---

# ═══════════════════════════════════════════
# POWERSHELL SCRIPTING
# ═══════════════════════════════════════════

### Problem P.1 — Redirection Operators ⭐⭐⭐
Explain the operational difference between the `>` operator and the `>>` operator when writing data to a text file. What happens to the target file in each scenario if it already contains data?

<details>
<summary>🔓 Click to reveal solution</summary>

**`>` operator (overwrite):**
- Writes output to the specified file
- If the file already exists and contains data, **all existing data is replaced** (overwritten) with the new output
- The file ends up containing ONLY the new output

**`>>` operator (append):**
- Writes output to the specified file
- If the file already exists and contains data, the new output is **added after** the existing data
- The file ends up containing the old data PLUS the new output

**Example:**
```powershell
# File has "Hello"
echo "World" > file.txt    # File now has only "World"
echo "World" >> file.txt   # File now has "World\nWorld"
```

</details>

---

### Problem P.2 — The Pipeline ⭐⭐⭐
Describe what happens to data when it is passed through the pipeline operator (`|`). Practice this relationship using Get-Process and Sort-Object as a practical example.

<details>
<summary>🔓 Click to reveal solution</summary>

The pipeline operator `|` passes the **output objects** of one command as **input objects** to the next command. In PowerShell (unlike traditional text-based shells), **objects** are passed — not text streams.

**How it works:**
1. The first command produces output objects
2. The `|` operator takes these objects and feeds them to the second command
3. The second command processes the objects and produces its own output

**Practical example:**
```powershell
Get-Process | Sort-Object -Property ID
```
- `Get-Process` retrieves all running processes as **process objects** (each has properties like ID, Name, CPU, etc.)
- `|` passes these process objects to Sort-Object
- `Sort-Object -Property ID` sorts the objects by the ID property (ascending by default)

The result is a list of all running processes sorted from lowest to highest Process ID.

</details>

---

### Problem P.3 — Comparison Operators ⭐⭐⭐
In PowerShell, regular mathematical symbols like `==` or `<` are not used for comparisons. State the correct PowerShell comparison operators for the following:
- Equals to
- Not equal to
- Greater than
- Less than or equal to

<details>
<summary>🔓 Click to reveal solution</summary>

| Meaning | PowerShell Operator |
|---------|-------------------|
| Equals to | `-eq` |
| Not equal to | `-ne` |
| Greater than | `-gt` |
| Less than or equal to | `-le` |

**Full comparison operator list:**
| Operator | Meaning |
|----------|---------|
| `-eq` | Equal to |
| `-ne` | Not equal to |
| `-gt` | Greater than |
| `-ge` | Greater than or equal to |
| `-lt` | Less than |
| `-le` | Less than or equal to |
| `-like` | Pattern matching with wildcards |

</details>

---

### Problem P.4 — Error Handling ⭐⭐
When running Get-Service, querying a non-existent service results in a terminating or non-terminating error that halts clean output. Name the parameter used to suppress this behavior, and explain how it allows an If-Else block to gracefully handle "missing" items.

<details>
<summary>🔓 Click to reveal solution</summary>

**Parameter:** `-ErrorAction SilentlyContinue`

**How it works:**
```powershell
$svc = Get-Service -Name "NonExistentService" -ErrorAction SilentlyContinue
if ($svc -eq $null) {
    Write-Host "Service not found"
} else {
    Write-Host "Service status: $($svc.Status)"
}
```

Without `-ErrorAction SilentlyContinue`, querying a non-existent service produces an error that disrupts the script output. With this parameter, the error is suppressed — the command simply returns `$null` instead of throwing an error. This allows the If-Else block to check if the result is `$null` and handle the "missing" case gracefully with a user-friendly message, instead of showing a raw error.

</details>

---

### Problem P.5 — Array and ForEach Script ⭐⭐⭐
Construct a Windows PowerShell script consisting of an array with 5 elements of odd number values beginning with 1. Using a foreach loop, print out these 5 elements to the console screen using the echo command. Name this script as Revision.ps1

<details>
<summary>🔓 Click to reveal solution</summary>

```powershell
# Revision.ps1
$numbers = @(1, 3, 5, 7, 9)

foreach ($num in $numbers) {
    echo $num
}
```

**Output:**
```
1
3
5
7
9
```

**Key points:**
- `@()` creates an array in PowerShell
- `foreach ($element in $array)` iterates through each element
- `echo` is an alias for `Write-Output`
- The script is saved as `Revision.ps1`

</details>

---

### Problem P.6 — Write a Service Audit Script ⭐⭐⭐
Write a PowerShell script that:
1. Creates an array of services: 'WinDefend', 'Spooler', 'wuauserv'
2. Uses ForEach to check each service
3. Displays Running services in Green, Stopped in Yellow, and missing/other in Red

<details>
<summary>🔓 Click to reveal solution</summary>

```powershell
$services = @('WinDefend', 'Spooler', 'wuauserv')

foreach ($service in $services) {
    $svc = Get-Service -Name $service -ErrorAction SilentlyContinue
    if ($svc -eq $null) {
        Write-Host "$service : Not Found" -ForegroundColor Red
    }
    elseif ($svc.Status -eq 'Running') {
        Write-Host "$service : Running" -ForegroundColor Green
    }
    elseif ($svc.Status -eq 'Stopped') {
        Write-Host "$service : Stopped" -ForegroundColor Yellow
    }
    else {
        Write-Host "$service : $($svc.Status)" -ForegroundColor Red
    }
}
```

</details>

---

### Problem P.7 — Process Sorting and File Output ⭐⭐⭐
Write PowerShell commands to:
1. Get all running processes
2. Sort them by ID (lowest to highest)
3. Save to `report.txt`
4. Append a timestamped "Done" message

<details>
<summary>🔓 Click to reveal solution</summary>

```powershell
Get-Process | Sort-Object -Property ID > report.txt
echo "Done - $(Get-Date)" >> report.txt
```

**Breakdown:**
- `Get-Process` — retrieves all running processes
- `Sort-Object -Property ID` — sorts by Process ID (ascending)
- `>` — redirects (overwrites) output to report.txt
- `>>` — appends the timestamped message to report.txt
- `$(Get-Date)` — embeds the current date/time in the string

</details>

---

### Problem P.8 — MCQ: PowerShell Array Syntax ⭐
How do you create an array in PowerShell?

A) `array(1, 2, 3)`
B) `[1, 2, 3]`
C) `@(1, 2, 3)`
D) `{1, 2, 3}`

<details>
<summary>🔓 Click to reveal solution</summary>

**C)** `@(1, 2, 3)`

The `@()` operator creates an array in PowerShell. Examples:
```powershell
$numbers = @(1, 2, 3, 4, 5)
$names = @('Alice', 'Bob', 'Charlie')
```

</details>

---

### Problem P.9 — MCQ: PowerShell String Interpolation ⭐
What happens when a variable name is used inside a double-quoted string in PowerShell?

A) It causes an error
B) The variable name is treated as literal text
C) The variable is replaced with its actual value
D) The variable is converted to uppercase

<details>
<summary>🔓 Click to reveal solution</summary>

**C)** The variable is replaced with its actual value.

```powershell
$name = "World"
Write-Host "Hello $name"    # Output: Hello World
Write-Host 'Hello $name'    # Output: Hello $name (single quotes = no interpolation)
```

Variable names within double-quoted strings are replaced with their values. Single-quoted strings treat everything as literal text.

</details>

---

# ═══════════════════════════════════════════
# SCENARIO-BASED QUESTIONS (Professor Style)
# ═══════════════════════════════════════════

### Problem S.1 — Integrated Scenario ⭐⭐⭐
A web server is running multiple processes. Each process handles one client connection. The server has 4GB of RAM but the total memory needed by all processes exceeds 8GB. Users report the system is extremely slow. Explain what is likely happening, using concepts from Chapters 1, 4, and 5.

<details>
<summary>🔓 Click to reveal solution</summary>

**The system is likely thrashing.**

Here's the analysis using course concepts:

**From Ch5 (Virtual Memory):** The total memory needed (8GB) exceeds physical RAM (4GB). The system uses virtual memory to compensate. However, the **sum of all active localities > total memory size**, which is the cause of thrashing.

**From Ch5 (Thrashing):** Each process needs pages that aren't in memory. When one process page-faults, the OS replaces a page from another process — but that process needs that page too. Processes spend more time **paging than executing**. CPU utilization drops.

**From Ch4 (Process States):** Processes are constantly moving between **Running → Blocked** (waiting for page I/O) **→ Ready** (page loaded) **→ Running** (briefly) **→ Blocked** again. Most time is spent in Blocked state.

**From Ch1 (Multiprogramming):** The OS may try to increase multiprogramming (add more processes), thinking the CPU is idle — but this makes thrashing worse because there's even less memory per process.

**Solution:** Use a local replacement algorithm, reduce the number of concurrent processes, or add more physical RAM.

</details>

---

### Problem S.2 — Integrated Scenario ⭐⭐⭐
A programmer writes a user program that directly tries to execute an I/O instruction to read from a hard disk. What happens and why? Use concepts from Chapters 2 and 3.

<details>
<summary>🔒 Click to reveal solution</summary>

**The program will fail** because I/O instructions are **privileged instructions**.

**From Ch2 (Processor Modes):** The user program runs in **user mode**, which can only execute non-privileged instructions. I/O instructions are privileged because they directly control hardware. The processor will **trap** (generate an exception) when the user program tries to execute the I/O instruction.

**From Ch2 (Kernel & System Calls):** To perform I/O, the user program must use a **system call** — calling a stub function provided by the OS, which executes a trap instruction to switch to **supervisor mode**. The OS kernel then executes the I/O on behalf of the program.

**From Ch3 (Device Controllers):** The I/O operation goes through the **device controller**, which has data registers, command registers, and status flags. The OS (Device Manager) manages this interface — user programs cannot access it directly.

**From Ch2 (Why Privileged):** If user programs could execute I/O directly, they could bypass security, read/write any device, corrupt data, and interfere with other processes' I/O operations.

</details>

---

### Problem S.3 — Integrated Scenario ⭐⭐⭐
Explain the complete journey of a system call from a user program to the OS and back, using concepts from Chapters 2, 3, and 4.

<details>
<summary>🔓 Click to reveal solution</summary>

**Step-by-step journey:**

1. **User program (Ch4):** A process in **user mode** needs to perform a privileged operation (e.g., read a file). It calls a function like `fork()`.

2. **Stub function (Ch2):** The OS provides a **stub function** that appears as an ordinary function call. The stub prepares the system call number and parameters.

3. **Trap instruction (Ch2):** The stub executes the **trap instruction**, which:
   - Switches the processor from **user mode** to **supervisor mode**
   - Branches to the **trap table** to find the entry point of the system function

4. **Kernel execution (Ch2):** The OS kernel function (e.g., `sys_fork()`) executes in **supervisor mode** with full access to all instructions and memory.

5. **Hardware interaction (Ch3):** If the system call involves I/O, the kernel interacts with the **device controller** — writing to command registers, checking status flags, or setting up **DMA** for data transfer.

6. **Return (Ch2):** On completion, the processor switches back to **user mode** and control returns to the user process.

7. **Context (Ch4):** If the system call blocks (e.g., waiting for I/O), a **context switch** occurs — the process moves from Running to Blocked state, and another process gets the CPU.

</details>

---

# ═══════════════════════════════════════════
# QUICK-FIRE ROUND (One-Line Answers)
# ═══════════════════════════════════════════

### QF.1
**Q:** What is the OS?
<details><summary>🔓</summary> A program that acts as an intermediary between user and hardware </details>

### QF.2
**Q:** Space-multiplexed example?
<details><summary>🔓</summary> Memory — each process gets its own distinct memory space </details>

### QF.3
**Q:** Time-multiplexed example?
<details><summary>🔓</summary> CPU — processes take turns using it </details>

### QF.4
**Q:** What mode does the kernel run in?
<details><summary>🔓</summary> Supervisor mode </details>

### QF.5
**Q:** What instruction switches user→supervisor mode?
<details><summary>🔓</summary> Trap instruction </details>

### QF.6
**Q:** System call or message passing — which is more efficient?
<details><summary>🔓</summary> System call </details>

### QF.7
**Q:** UNIX kernel type?
<details><summary>🔓</summary> Monolithic </details>

### QF.8
**Q:** Von Neumann architecture components?
<details><summary>🔓</summary> CPU (ALU + CU), Primary Memory, I/O Devices, Buses </details>

### QF.9
**Q:** What does the ALU do?
<details><summary>🔓</summary> Performs arithmetic and logical operations </details>

### QF.10
**Q:** What does the control unit follow?
<details><summary>🔓</summary> Fetch-execute cycle </details>

### QF.11
**Q:** 3 registers for CPU-memory interface?
<details><summary>🔓</summary> MAR (address), MDR (data), CMD (command) </details>

### QF.12
**Q:** Polling wastes what?
<details><summary>🔓</summary> CPU cycles (busy-wait) </details>

### QF.13
**Q:** DMA allows what?
<details><summary>🔓</summary> Device to read/write memory without CPU intervention </details>

### QF.14
**Q:** What is a process?
<details><summary>🔓</summary> A binary program in execution </details>

### QF.15
**Q:** What is a thread?
<details><summary>🔓</summary> A single execution engine in a program </details>

### QF.16
**Q:** Threads share what?
<details><summary>🔓</summary> Code, data, resources </details>

### QF.17
**Q:** Threads don't share what?
<details><summary>🔓</summary> Program counter, registers, stack, status </details>

### QF.18
**Q:** What is a PCB?
<details><summary>🔓</summary> Process Control Block — data structure storing process info </details>

### QF.19
**Q:** Context switch requires?
<details><summary>🔓</summary> Trap or interrupt to give OS control of CPU </details>

### QF.20
**Q:** 4 basic process states?
<details><summary>🔓</summary> Running, Ready, Blocked, Done </details>

### QF.21
**Q:** What is virtual memory?
<details><summary>🔓</summary> Using disk to supplement RAM, allowing processes not completely in memory </details>

### QF.22
**Q:** What is locality?
<details><summary>🔓</summary> Tendency of programs to use only a small portion of code/data at a time </details>

### QF.23
**Q:** What is a page?
<details><summary>🔓</summary> Fixed-size block of virtual addresses (size = 2^h) </details>

### QF.24
**Q:** What is a page fault?
<details><summary>🔓</summary> Accessing a page not in primary memory </details>

### QF.25
**Q:** What does the valid-invalid bit indicate?
<details><summary>🔓</summary> 1 = page in memory, 0 = page on disk </details>

### QF.26
**Q:** What is thrashing?
<details><summary>🔓</summary> Process spends more time paging than executing </details>

### QF.27
**Q:** PowerShell equals operator?
<details><summary>🔓</summary> `-eq` </details>

### QF.28
**Q:** `>` does what to file?
<details><summary>🔓</summary> Overwrites </details>

### QF.29
**Q:** `>>` does what to file?
<details><summary>🔓</summary> Appends </details>

### QF.30
**Q:** Pipeline passes what?
<details><summary>🔓</summary> Objects (not text) </details>

### QF.31
**Q:** Suppress errors in Get-Service?
<details><summary>🔓</summary> `-ErrorAction SilentlyContinue` </details>

### QF.32
**Q:** PowerShell array syntax?
<details><summary>🔓</summary> `@()` </details>

### QF.33
**Q:** PowerShell is case sensitive? (True/False)
<details><summary>🔓</summary> False </details>

### QF.34
**Q:** What is demand paging?
<details><summary>🔓</summary> Pages loaded only when needed </details>

### QF.35
**Q:** Dirty bit purpose?
<details><summary>🔓</summary> Only modified pages written back to disk </details>

---

*Study these problems until you can answer without clicking the solutions. Good luck!* 🎓
