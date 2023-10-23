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

  Certainly! It seems you've provided a summary representation of the slides. I'll correct and improve the transcription based on the details you provided:

---

# **Chapter 3 : Memory Management**  
*[ Organizing Processes in Main Memory ]*

**1. Introduction**  
**2. Processor**  
**3. Input/Output Devices**  
**4. Communication Bus**  
**5. Memory**  
- Optimal use of the processor → multiple processes share memory  
- The OS must determine: 
    1. Which processes are present in memory
    2. How they are organized  

**Memory Management**  
*Address Translation*  
*[ handled by the loader, assisted by the linker ]*

- **At compile time:** Absolute/physical address, location is rigid.
- **At load time:** Relative/logical addresses mapped to absolute, once translated location is fixed.
- **At run-time:** Relative/logical addresses, location is flexible.

**Memory Management**  
*Memory Organization*  
- Part of the memory will be reserved for the OS.
- Focus: management of memory to be shared by different user processes.
- Three main alternatives:
    - **Partitioning**
    - **Paging**
    - **Segmentation**

**Partitioning**  
- **Fixed Partitioning – Fixed Size:** Divide memory into partitions of fixed size. Each process image gets a partition assigned. Issues include internal fragmentation (~half of the partition is unused), processes too large to fit, and limitations on the max. size of process image and number of processes in memory. Solution: partitions of multiple sizes.
- **Fixed Partitioning – Variable Size:** Less internal fragmentation. Challenges include deciding where to add each process.
- **Placement Algorithm:** Options include waiting for an available partition or taking a sufficiently large partition.
- **Dynamic Partitioning:** Create partitions dynamically. Challenges include memory holes (external fragmentation).
- **Buddy System:** Divide and combine memory blocks dynamically, achieving ~75% memory usage.

**Paging**  
- **Description:** Divide memory and process images into fixed-size blocks (pages). Advantages: no external fragmentation and small internal fragmentation.
- **Memory Translation:** Logical address translation using process page tables.
- **x86 Paging:** Specific details on x86 architecture paging.

**Segmentation**  
- **Description:** Similar to paging but with variable-size segments. Advantages: no internal fragmentation. Potential issue: external fragmentation.
- **Memory Translation:** Logical address translation using process segment tables.
- **x86 Segmentation:** Details on x86 segmentation.

**Key Points**  
- Advantages and disadvantages of fixed and dynamic partitioning.
- Placement algorithms.
- Buddy system.
- Paging and Segmentation.

### Disambuguation for key points:

1. **Advantages and Disadvantages of Fixed and Dynamic Partitioning**

   - **Fixed Partitioning**:
     - **Advantages**:
       - **Simplicity**: Memory is divided into fixed sizes, which makes it easy to manage.
       - **Predictability**: Since partitions are fixed, allocation and deallocation are consistent.
     - **Disadvantages**:
       - **Internal Fragmentation**: A process may not use all the space in a fixed partition, leading to wasted memory.
       - **Limitation on Process Size**: Processes larger than a partition size cannot be accommodated.
       - **Limitation on Number of Processes**: The number of processes that can be loaded into memory is constrained by the number of partitions.

   - **Dynamic Partitioning**:
     - **Advantages**:
       - **Flexibility**: Partitions are created based on the exact size required by the process, ensuring efficient utilization.
       - **Accommodates Larger Processes**: Since partitions are dynamic, larger processes can be accommodated.
     - **Disadvantages**:
       - **External Fragmentation**: Over time, free memory blocks ("holes") can become scattered, making it hard to find contiguous memory for new processes.
       - **Complexity**: Dynamic partitioning requires more sophisticated memory management techniques.

2. **Placement Algorithms**:
   
   - Used mainly in the context of Dynamic Partitioning to decide where in memory a process should be loaded.
     - **Best-fit**: Places the process in the smallest free partition that fits the process. This can produce many small unallocated holes.
     - **First-fit**: Places the process in the first available partition that is large enough. It can be faster but may not make the most optimal use of memory.
     - **Next-fit**: Similar to first-fit, but starts the search from the location of the last placement.
     - **Worst-fit**: Places the process in the largest available partition, based on the idea that this large partition can accommodate future processes.

3. **How does the Buddy System Work?**
   
   - The **Buddy System** is a memory allocation scheme.
     - **Memory Size Consideration**: Memory size is considered as powers of two. If a block of a needed size is not available, existing blocks are divided recursively.
     - **Dynamic Division and Combination**: If the exact block size isn't present, a larger block is split recursively until the desired size is achieved. Conversely, when a block is freed, it can be combined with its "buddy" (adjacent block of the same size) to form a larger block.
     - This system tries to minimize fragmentation by ensuring that blocks are always split and coalesced in a structured manner.
     - On average, the Buddy System achieves about 75% memory usage efficiency.

4. **Paging and Segmentation and their Relationship to Fixed and Dynamic Partitioning**:

   - **Paging**:
     - Divides both physical memory and process memory into fixed-size blocks called frames and pages, respectively.
     - It provides a way to manage memory in a fixed-size manner similar to fixed partitioning but is more flexible due to its ability to swap pages in and out.
   
   - **Segmentation**:
     - Divides memory into segments of variable sizes, based on the requirements of different parts of a program or data structures.
     - It offers variable partitioning much like dynamic partitioning.
   
   - **Relationship**:
     - **Fixed Partitioning vs. Paging**: Both deal with fixed sizes, but paging offers more flexibility and eliminates external fragmentation.
     - **Dynamic Partitioning vs. Segmentation**: Both allow variable-sized divisions, but segmentation aligns more closely with logical divisions in a program or dataset.

