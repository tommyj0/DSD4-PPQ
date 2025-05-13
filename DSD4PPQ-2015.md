# Digital System Design 4 2015

## A1

### a)

i. 

RISC stands for Reduced Instruction Set Computing.

The increase in market share for RISC computers, when compared to CISC computers is due to the rise of mobile and embedded devices which are more catered to executing many simple instructions, rather than the few complicated ones found in CISC computing. The popularity of ARM is also an important factor in the recent rise of RISC computing, due to their extensive line of RISC cores and open licensing.

ii. 

Pipelining allows functional units of the CPU to be used simultaneously, reducing the clock time, thus increasing throughput. This increases functional unit utilisation when compared to a single cycle implementation. Say something about exploiting parallelism...

### b)

i. 

Static MI approaches don't reorder the execution of instruction, thus relying on the compiler to reorder the instructions in the most efficient way.

Whereas Dynamic MI approaches can change the order of execution at runtime, increasing the complexity of the hardware required to avoid hazards and stalls, increasing speed.

ii. 

Loop unrolling is the process of creating an equivalent loop that executes more than one iteration in each loop, often using different registers names. This increases code size, but can increase performance by reducing the number of branches and increasing parallelism within the loop.

### c)

i. 

Amdahl's Law

ii. 

Strong Scaling improves fixed-sized problems, where speed increases come at the cost of the efficiency

Weak scaling maintains the same speed, but efficiency decreases as the size of the problem increases.

### d)

i. 

Fine-Grain MT. It switches between threads on every cycle. Thread stalls can be serviced while other threads are being executed.

ii. 

SMT:

15

|Slot 1|Slot 2|Slot 3|Slot 4|
|---|---|---|---|
|1|1|1|2|
|2|3|1|1|
|1|1|2|2|
|2|3|3|1|
|1|3|3|3|
|1|2|2|2|
|2|1|1|1|
|2|3|3||
|2|3|||
|2|3|3|3|
|3|1|1|2|
|2|3|3|3|
|1|1|3|3|
|2|3|||
|1|1|1||

Fine-Grain:

7+8+9=24

Speedup = 24/15 = 1.6x 

### e)

i. 

Memory Bandwidth 

ii. 

honestly idk. Could either be due to poor memory bandwidth or reduced floating point performance.

Increase Memory usage by leveraging software prefetching or increasing memory affinity

Increasing floating point performance can be done by: balancing adds and multiplies, and improving the instruciton level parallelism and use of SIMD.

## B1

### a)

i. 

Increase the performance by storing recently used and nearby memory in a much faster SRAM block (rather than the more space efficient DRAM used in main memory).

ii. 

Spatial locality: memory accesses near to each other are more likely to hit as, depending on the block size, nearby memory is also loaded on a hit. This type of locality is exploited in contiguous arrays (data cache) and sequential code execution (instruction cache).

Temporal Locality: Nearby memory accesses performed close to each other will increase the chance of a cache hit as recently used data is stored in the cache. Loops result in recently used data being reused (data cache) and recently loaded instructions being rerun (instruction cache)

iii. 

Spatial: any contiguous block of memory, such as an array, benefits from this arrangement as nearby elements will be loaded within cache blocks, hence increasing access speed.

Temporal: Loops in software result in the same instructions, and often the same data, being used in a short span of time. The cache speeds the subsequent accesses up by storing the most recently used elements.

iv.

branching/jumping to far away subroutines, accessing instructions which would not be in the same block.

### b)

i.

The access time could increase due to the increased hardware required to check all tags in an set. The chance of conflict misses are reduced, decreasing the miss rate. LRU becomes more complex (or has to be introduced if starting from DM) when replacing blocks, increasing the miss penalty. 

Decreasing block size, thus increasing the index potentially increasing hit time. Miss rate could increase or decrease depending on the current block size. Typically, there is a sweet spot for block sizes ~64B, going much lower increases the compulsory misses and going to large, may increase conflict misses due to pollution. Miss penalty will be decreased as less data is fetched.

### c)

Block size = 32B

Cache Size = 64KiB

Block No. = 2048

Block Offset (Byte Offset) = 5b 

Set associativity = 4-way

Sets = 512

Index = 9b

Write Scheme = Write Back (Dirty bit for each block)

Replacement Policy = LRU (2 bits for each block)

i.

|Tag|Index|Block Offset|
|---|---|---|
|31:14|13:5|4:0|

ii.

Not drawing a diagram

For each block:

|V(1b)|D(1b)|LRU(2b)|Tag(16b)| Data (32B)|
|---|---|---|---|---|

## B2

### a)

>N.B. This Q doesn't make complete sense in RV. Change wording from "word-aligned addressing" to "Base Addressing"

PC-relative addressing involves using a the current PC and an immediate to fetch data, examples include branch and jump instructions.

Base Addressing uses a register and an immediate, creating an address that can be used to fetch data from memory, examples include load and store operations.

### b)

>N.B. again just assume branch and jump in RV and ignore shift-left-by-2 stuff as it isn't the case in RV :)

i.

Branch instructions give 13 bits of 2'sC range meaning the max address is:

$$
PC = 0\textrm{x}000 + 2^{12}-1=0\textrm{x}00000FFE
$$

and min address:

$$
PC = 0\textrm{x}000 - 2^{12}=0\textrm{x}FFFFF000
$$

ii.

Jump instructions give 21 bits of 2'sC range meaning the max address is:

$$
PC = 0\textrm{x}00000 + 2^{20}-1=0\textrm{x}000FFFFE
$$

and min address:

$$
PC = 0\textrm{x}00000 - 2^{20}=0\textrm{x}FFF00000
$$

### c)

> Can't really be converted to RV, skip Q

### d)

> Use x1,x2,x3 instead of $s0,$s1,$s2 because x0 is hardwired to 0

    // x1 = x
    // x2 = y
    // x3 = result

    mul x4,x1,x1 // x4 = x^2
    mul x3,x4,x1 // x3 = x^3
    addi x5,x0,6 // x5 = 6
    mul x4,x4,x5 // x4 = 6x^2
    mul x4,x4,x2 // x4 = 6x^2y
    add x3,x3,x4 // x3 = x^3 + 6x^2y
    mul x4,x2,x2 // x4 = y^2
    mul x4,x4,x2 // x4 = xy^2
    addi x5,x0,12 // x5 = 12
    mul x4,x4,x5 // x4 = 12xy^2
    add x3,x3,x4 // x3 = x^3 + 6x^2y + 12xy^2
    mul x4,x2,x2 // x4 = y^2
    mul x4,x4,x2 // x4 = y^3
    slli x4,x4,3 // x4 = 8*y^3
    add x3,x3,x4 // x3 = x^3 + 6x^2y + 12xy^2 + 8y^3

## B3

### a)

> Swap MIPS for RV

Instruction Fetch (IF): Program counter is incremented or set to the appropriate branch/jump offset. Instruction is read using the PC, from the instruction memory, as the address and passed onto the next stage.

Instruction Decode (ID): Control signals are generated from instructions. Registers are read from the register file and passed onto the next stage.

Execute (EXE): The ALU performs any necessary operations. Branch and jump addresses can also be calculated in this stage.

Memory Access (MEM): Load and Stores are performed on the data memory

Write Back (WB): Registers are updated in the register file.

Architecture: RV is an ISA **not** an implementation, therefore Harvard and Von Neumann architectures are both valid implementation for the ISA. 

Von Neumann archs only contain one bus between the CPU and memory, creating a structural hazard, also known as the Von Neumann Bottleneck, preventing instruction and data memory from being accessed simultaneously. 

Splitting the buses, such as in Harvard and Modified Harvard archs, allows both memories to be accessed at the same time, avoiding stalls when IF and MEM stages overlap. 

Modern CPUs have to use a Von Neumann architecture at the interface between the CPU and main memory, due to the OS storing instruction and data together, creating programs. This bottleneck can be bypassed by splitting the data and instruction cache at L1, creating a Harvard style architecture at the interface between the Pipeline and Cache (which together comprise the CPU), allowing both instruction and data to be accessed at the same time.

### b)

i. 

LW and SW instructions:

$$
25 + 15 = 40\% \textrm{data-mem usage}
$$

ii.

all 3 ports will only be used in R-format instructions, which is ADD = 20%.

Also worth noting that the reg_write port is not used in the same cycle as the reads, reads are performed in ID, writes are performed in WB.

iii.

The branch adders runs regardless of whether there is a branch instruction or whether it is taken or not. To calculate the total percentage of taken branchs:

$$
40*0.25 = 10\%
$$

### c)

> Diagrams are in the notes

SISD: the simplest architecture to implement, poor performance, typically used in single core embedded applications

SIMD: increasing data output for a low instructions count in scenarios where one operation must be applied to an array of values. Concept which GPUs are built upon. The RV vector extension reduces instruction count and execution time by applying an operation to a vector register (basically an array in the reg file).

MISD: Increase reliability by introducing redundancy and error checking. Uncommon architecture, but can be used to build a fault-tolerant computer.

MIMD: Reading multiple instructions in a cycle, then extending the principle of SIMD to parallelise the execution of these instruction. Modern CPUs are good examples of this concept, utilising multiple-issue units (multiple instructions) and vector operations (multiple data).

