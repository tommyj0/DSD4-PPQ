# Digital System Design 4 2017

## A1

### a)

i.

RISC stands for Reduced Instruction Set Computing.

The increase in market share for RISC computers, when compared to CISC computers is due to the rise of mobile and embedded devices which are more catered to executing many simple instructions, rather than the few complicated ones found in CISC computing. The popularity of ARM is also an important factor in the recent rise of RISC computing, due to their extensive line of RISC cores and open licensing.

ii.

Pipelining allows functional units of the CPU to be used simultaneously, reducing the clock time, thus increasing throughput. This increases functional unit utilisation when compared to a single cycle implementation. Say something about exploiting parallelism...

### b)

Diagram would just be the standard VN arch.

VN bottleneck arises from the inability to access instruction and data memory at the same time (as the bus is unified), meaning that in a pipelined processor IF and MEM stages cannot be completed simultaneously creating a structural hazard that requires many stalls as a large portion of instructions use data memory and all instructions use instruction memory.

Harvard architectures solve this by splitting the data and instruction **buses**, with the standard Harvard also splitting the memories, and modified harvard using a unified memory. Both these H implementations avoid the structural hazard posed by the VN implementations, allowing the IF and MEM stage to be executed in parallel.

### c)

i.

> Not easy to translate to RV

ii.

> x1 stores i, x2 stores j, x3 stores k,

LOOP:   bge x1,x2,DONE // if i >= j : PC = DONE
        addi x3,x3,1 // k++
        add x1,x1,x1 // i = i + i (equivalent and faster than i*2)
        j LOOP // Unconditional jump to LOOP
DONE:

iii.

> Question is slightly weird, bge is a pseudo instr in MIPS but not in RV. Question has been answered generally and then for branch pseudos and jump pseudos

Pseudo instructions provide a small layer of abstraction from the instructions implemented in hardware, representing one or more hardware instruction

Branch instructions, like "bgt", are not implemented in HW, but can instead be translated to "ble", when assembling.

Jump instructions with no link, like "j", are implemented by using "jal" and linking to x0 (discarding the return address)

### d)

i.

3248674260 = 0xC1A2D5D4

Reverse address is:

0xC1A2D5D4 - 0x1000 = 0xC1A2C5D4

ii.

> No shift-left-by-two in RV but same thing kind of happens with shifting imm address left by one

Shifting the address to the left by one is required in most RV implementations as the smallest possible instruction is 2B long (Compressed extension), so the final byte is never needed for instruction addressing so it is implied as 0.

## B1

### a)

i.

maybe draw a diagrams showing the levels

|Memory Level|Storage Size|Speed|Notes|
|---|---|---|---|
|Hard Disk|Very Large (100GiB -> 100TiB) | Slow (5 -> 20ms)|Electromagnetic Spinning Disk|
|Flash SSD|Large (64GiB -> 10TiB) | Moderate (5 -> 50microns)|Solid State|
|RAM|Small (4GiB -> 64GiB) | Fast (50ns -> 70ns)| Capacitor and transistor pair|
|Cache|Very Small (KiBs -> MiBs) | Very Fast (0.5ns -> 2.5ns)|SRAM cells close to CPU|

The aim of the hierarchical design is to obtain the speed of cache with the size of a HD. This is done by storing more recently used memory in the smaller and faster levels of memory, achieving near cache performance (on average) with Hard Disk level space.

ii.

Spatial locality: memory accesses near to each other are more likely to hit as, depending on the block size, nearby memory is also loaded on a hit. This type of locality is exploited in contiguous arrays (data cache) and sequential code execution (instruction cache).

Temporal Locality: Nearby memory accesses performed close to each other will increase the chance of a cache hit as recently used data is stored in the cache. Loops result in recently used data being reused (data cache) and recently loaded instructions being rerun (instruction cache).

### b)

i.

Block size = 64B

Block No. = 32KiB/64B = 512 Blocks

ii.

Block offset (Bytes) = 6b

Block index = 9b

Tag = 32-9-6 = 17b

iii.

Set No. = 512/8 = 64

Block offset (Bytes) = 6b

Block index = 6b

Tag = 32 - 6 - 6 = 20b

iv.

Hit time would increase as more block tags need to be checked and compared to the requested access

### c)

i.

> Assuming each access is a half-word (2B) access

Each access is separated by 2. Block size is 64B. 31 accesses will be covered by the first miss. Miss rate:

$$
\frac{1}{32} = 3.125\%
$$

ii.

Miss rate won't change through greater associativity. Associativity benefits from temporal locality, allowing greater flexibility for far away memory accesses.

This use-case is an example of high spatial locality. The Block size is responsible for improving the miss rate, determining how many sequential elements are loaded after the initial cold/compulsory miss.

## B2


