# Operating-Systems

--- 
## Week 1

## Operating Systems: Introduction

### Definitions:
1. **Operating System (OS)**: Acts as an intermediary between users and the hardware. It provides an environment for the proper use of programs, balancing convenience and efficiency.
2. **Computer System (Abstract View)**:
    - System and Application Programs
    - Operating System
    - Computer Hardware
    - Users (user-1, user-2, ... user-n) and their respective applications (compiler, media player, text editor, database system, etc.)
3. **A User Perspective**:
    - **Single-user Scenario**: Designed for the monopolization of its resources. It prioritizes high performance and low resource utilization.
    - **Multi-user Scenario**: Resources are shared among users, leading to high resource utilization and lower performance.
4. **A System Perspective**:
    - OS acts as a manager of resources ensuring efficient and fair operation.
    - OS controls the execution of programs, prevents errors, and manages the operation/control of I/O devices.
5. **Common Definition**: The program running at all times on the computer. The distinction between system programs (associated with the OS) and application programs (not associated) can be blurry.

---

## Operating Systems: Processes and Threads

### Definitions:

1. **Modern Computer System**:
    - Main components: Input/Output Devices, Communication Bus, Processor, and Memory.
    - **Processor Task**: Executes machine instructions which are sets of bits of fixed length (e.g., 16/32/64 bits). Instructions have opcodes like ADD, MOV, etc. There are RISC and CISC types of processors.
    - **Interruption Mechanism**: Signals the occurrence of an event. This can be done in software via a system call.
    - **Instruction Cycle**: Essential for maximizing processor efficiency in multi-program systems.
2. **Process**:
    - Defined as a "program in progress".
    - Attributes: Text (code) of the process, static/dynamic data, user stack (plus kernel stack), and process control block. Together, these define the process image.
    - **User Stack**: Supports recursive procedure calls, stores return addresses, local variables, parameters, frame pointer, and has pointers to the stack in the processor's registers.
    - **Process Control Block (PCB)**: Contains information needed by the OS for process management. This includes process identification (process-id, user-id, parent-id), processor state information (related to processor registers), and process control information (state, privileges, memory info, etc.). PCBs are stored in the OS's process tables.
    - **Process States**: 
        - **Running**: The process has access to the CPU.
        - **Ready**: The process can use the CPU but is currently interrupted.
        - **Blocked**: The process needs to wait for input from a third party.
        - **Suspend/Swapped**: A mechanism to take advantage of the CPU by suspending certain processes under specific conditions.
    - **Privilege Levels**: 
        - **User Mode**: Limited set of instructions may be executed.
        - **Kernel Mode**: No restrictions.
3. **Threads**:
    - **Motivation**: Each process has associated resources and a set of instructions. A program can be seen as multiple processes. Threads allow for more efficient partitioning of a program.
    - **Definition**: Threads share resources like code/data and control block but follow different paths of execution. They have their own user/kernel stack.
    - **Processes vs. Threads**:
        - **Multiple Processes**: Slower creation and switching, requires OS for concurrency and communication/sharing, different process states, can be independently swapped.
        - **Multiple Threads**: Faster creation and switching, immediate information exchange, synchronization not guaranteed, one process state (for user-level threads), jointly swapped.
    - **Thread Implementations**:
        - **User-level Threads (ULT)**: Thread management is done by the process. The kernel isn't aware. Handled via a thread library.
        - **Kernel-level Threads (KLT)**: Thread management is handled by the kernel. Scheduling is at the thread level instead of the process level.

---

## Key Points:

1. Understand the main characteristics of Processes and Threads.
2. Be aware of process states and privilege levels.
3. Recognize the difference between Mode Switch and Process Switch and understand their importance.
4. Know the strengths and weaknesses of using multiple processes and multiple threads.

---

## Recommended Reading:

- Silberschatz et al., Operating System Concepts Essentials, 2nd Edition. Chapters 1, 3, and 4.

---

## Week 2 : Cache Memory

Understanding the principles behind operating systems' memory management is crucial, especially considering the discrepancy in speed between processors and storage devices.

### Key Components:
1. **Processor**
2. **Memory**
3. **Input/Output Devices**
4. **Communication Bus**

## Storage Hierarchy:
- **Properties**:
  - **Capacity**
  - **Speed**
  - **Cost**
- **Types**:
  - **Volatile**: Temporarily stores data (loses content when powered off).
  - **Nonvolatile**: Permanently stores data (retains content when powered off).
  - **Semiconductor memory**:
    - Contains both volatile and nonvolatile types.
    
**Note**: The relationships among capacity, speed, and cost are still in place.

### Why not always use the fastest memory components?
It's impractical due to cost and other factors. Memory hierarchy is designed based on these relationships to get the best balance.

## Memory Technology Evolution:
- **SRAM** is typically used for cache.
- **DRAM** is generally used for main memory.

## Locality of Reference:
Memory hierarchy's effectiveness is reliant on the principle of **locality of reference**, which includes:
- **Spatial locality**: e.g., arrays and program counters.
- **Temporal locality**: e.g., frequently accessed variables, loop constructs.

## Cache Connection:
Cache is an intermediary between memory and CPU, speeding up data access. The connection can be direct or through standard communication bus (potentially slower).

### Cache Organization:
- Memory is divided into M blocks with K words each.
- Cache has C lines, significantly less than M.
- Transfers are done in blocks, based on the **locality of reference** principle.

## Cache Operations:
- **Default hit ratio** is C/M.
- **Effect of block size**: 
  - Decreasing block size increases the number of cache lines, but might decrease the effect of spatial locality.
  - Increasing block size decreases the number of cache lines, affecting spatial locality differently.

## Mapping Functions:
- Used to link main memory with cache.
- **Types**:
  - **Direct Mapping**: A specific memory block has only one spot in cache.
  - **Associative Mapping**: Blocks can be written anywhere in cache.
  - **Set Associative Mapping**: Cache is divided into sets, with each block mapped to one set.

### Replacement Algorithms:
For caches that allow a memory block to be written in multiple places, there's a need for algorithms to decide which cached item to replace on a miss.
- **Random**: Simple but potentially inefficient.
- **FIFO**: Replaces the oldest cache line.
- **Least Recently Used (LRU)**: Replaces the least recently accessed line.
- **Pseudo LRU**: Tries to achieve LRU's performance with FIFO's simplicity.

## Memory Updates:
For ensuring cache and main memory synchronization:
- **Write Through**: All cache updates are directly updated in the main memory.
- **Write Back**: Only updated in main memory when the block is removed from cache.

## Current Cache Designs:
- Multiple levels of cache (L1, L2, L3).
- Cache can be split for instructions and data.
- Some systems use TLBs, which will be discussed further in a virtual memory lecture.

## Cache Benchmarking:
- Benchmarking helps in quantifying cache characteristics.
- Assumption for benchmarking is usually FIFO or LRU replacement policy.

## Takeaways:
- Memory hierarchy is a balancing act between speed, cost, and capacity.
- Cache helps bridge the speed gap between the processor and main memory.
- Understanding cache behaviors and policies is essential for optimal system performance.
