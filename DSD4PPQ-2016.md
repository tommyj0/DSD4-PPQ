# Digital System Design 4 2016

## A1

### a)

> idk what they're referring to here

1. Simple/Uniform instructions - each instruction performs a basic task and is the same length, simplifying decoding (generally less need to use a microcode - decode is hardwired)

2. Load/Store architecture - Memory access is limited to specific instructions

3. Large number of Registers - Minimise (slow) memory access by increasing the number of registers

4. Pipeline-Friendly Design - Instructions are design to be executed in a single cycle, minimising complexity and stalling

### b)

> Remember to round the CR down

i.

$$
\textrm{CR} = \frac{1}{170+350+100+160+150} = 1.07GHz
$$

ii.

$$
\textrm{CR} = \frac{1}{350ps} = 2.85GHz
$$

iii.

$$
\textrm{Speedup} = \frac{2.85}{1.07} = 2.66\textrm{x}
$$

iv.

Split ID, 350/2 = 175. So shortest stage would still be 175:

$$
\textrm{CR} = \frac{1}{175ps} = 5.71GHz
$$

splitting stages improves throughput but increases hardware complexity, due to the increased control signals and pipeline registers. Might also stall more due to the increased data dependencies.

### c)

Diagram would just be the standard VN arch.

VN bottleneck arises from the inability to access instruction and data memory at the same time (as the bus is unified), meaning that in a pipelined processor IF and MEM stages cannot be completed simultaneously creating a structural hazard that requires many stalls as a large portion of instructions use data memory and all instructions use instruction memory.

Harvard architectures solve this by splitting the data and instruction **buses**, with the standard Harvard also splitting the memories, and modified harvard using a unified memory. Both these H implementations avoid the structural hazard posed by the VN implementations, allowing the IF and MEM stage to be executed in parallel.

### d)

> blt is not a psuedo-instruction in RV, but ble is. Answer the Q replacing "blt" with "ble" 

"ble" would be implemented by swapping the source registers of the "bge" core instruction:

ble rs1,rs2,imm // if rs1 <= rs2 : PC = PC + {imm,1'b0} 

bge rs2,rs1,imm // if rs2 => rs1 : PC = PC + {imm.1'b0} 

### e)

i.

Arithmetic intensity is a measure of the floating point operations per byte of memory that must be fetched. Moving a file would be a low arithmetic intensity operation.

ii.

FLOPs/Byte = 2FLOPS/4B = 1/2

Processor B has better performance at 8 GFLOPs/sec

iii.

The memory bandwidth must be improved twofold.

This could be improved by implementing SW prefetching and increasing memory affinity

## B1

### a)

Virtual memory addressing abstracts the memory space of a process, by providing apparent contiguity (required when memory is fragmented), ensuring memory safety between processes, and increasing the apparent size of the memory beyond that available in RAM by demoting rarely used memory to disk.

### b)

i.

This situation is an example of cache speedup through temporal locality. The data and instructions used within this loop will likely be accessed more than once, thus after the compulsory misses further iterations should hit more frequently. This is possible as the cache stores the most recently used data and, in the case of associative caches, can choose to replace blocks that have been less frequently used than others.

ii.

This scenario is an example of spatial locality. A data array is typically stored in a contiguous series of addresses, meaning that accesses to the same array will result in a high hit rate as adjacent elements will be loaded along with the requested data (depending on the block size). 

### c)

i. 

Block size = 32w = 128B
Block No. = 16KiB/128 = 128

ii.

Set No. = 128/4 = 32

iii.

Index bits = log2(32) = 5

iv.

Block Offset = log2(128) = 7

Tag bits = 32 - 7 - 5 = 20

### d)

i.

Tag bits = 32 - 7 = 25
Block Offset = 7
No index

ii.

the set-associative cache would have a lower hit time, as the fully-associative cache has to compare more blocks.

iii.

Current block size is already large at 128B, increasing it further would result in a higher miss rate, due to increase pollution (recently loaded blocks overwriting useful data)

Hit time would increase as there would be fewer blocks to search through

iv.

There are 128 blocks in the "set", greatly increasing the complexity of an LRU implementation. The fastest and most memory efficient scheme would be Random or FIFO as in both cases no extra bits are required, FIFO would be more efficient, but also require more hardware. Considering the size of the set, it is likely that a random scheme would perform very similarly to the other schemes and requires the least amount of hardware.

## B2

### a)

Amdahl's Law determines the maximum theoretical speedup through increased paralellisation, taking into account the parallelisable portion of the workload.

i.e. You can only parallelise the parallelisable part

$$
T_{sequential} + T_{parallel}/P \le T_p
$$

### b)

i.

Message Passing - Each processor has private physical address space, hardware sends/receives messages between processors. Video encoding would benefit from this topology

Shared Memory - Hardware provides single physical address space for all processors. Synchronise shared variables using locks. 


ii.



### c)

i.

UMA provides equal access time for all processors, giving lower latency for shared memory than NUMA. However speed is slower than NUMA local access.

NUMA can be appropriate for tasks that are partly localisable. There is a potential for performance bottlenecks when accessing memory that is not local to the processor, leading to increased latency.

ii.

35*4096 = 143,360 cycles

iii.

40*4096 = 163,840 cycles

iv.

if x = T/2 = 4096/2 = 2048:

$$
35*4096 > 15*2048 + R*2048 \rightarrow R < 55 \textrm{ cycles/word}
$$

## B3

### a)

> Ignore MIPS related stuff -> just assume SB and J format are referenced. Replace pseudo-direct addressing with Base addressing

i.

PC addressing - implemented by generating an immediate, then adding to the current PC value in the EXE stage. Use branch control signal to determine whether PC should be set to new value or incremented

Base addressing - Add the immediate value to rs1 in the EXE stage, and then either use to set value or use to address data memory. The value can also be set to the PC

ii.

Branch forward is 0xFFE

Jump forward is 0xFFFFE


### b)

Result has to be 1 bit wider than the input width, to catch any overflow. 

Zero detection can be done with combinational logic on the result register, ensuring result == 0 && overflow == 0.

### c)

i.

Input = opcode<5:0>

Outputs = AluSrc, RegWrite, RegDest...

no chance I'm doing the array

ii.

ditto






