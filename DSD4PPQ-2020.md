# Digital System Design 4 2019

## A1

### a)

Personal Gaming desktops should be catered to fast I/O, such as snappy mouse/keyboard inputs and short frame generation times. Latency is more important than throughput. even though multiple processes may be running concurrently, the time taken from registering an input to that output being serviced should be minimised. This leads to a lesser focus on parallelism (less core required) and a greater focus on raw thread execution time (higher clock speeds).

For a server in a cloud computing system, the most important metric of performance is the number of requests that can be serviced in a second, i.e. throughput. Throughput can be achieved by increasing the parallelism of the hardware and the parallisability of the load.

### b)

i.

$$
CPI_1 = 1*0.6 + 2*0.3 + 4*0.1 = 1.5
$$

$$
CPI_2 = 2*0.6 + 2*0.3 + 5*0.1 = 2.3
$$

ii.

$$
MIPS_1 = \frac{CR_1}{1M*CPI_1} = \frac{1000M}{1M*1.5} = 667MIPS
$$

$$
MIPS_2 = \frac{CR_2}{1M*CPI_2} = \frac{1150M}{1M*2.3} = 500 MIPS
$$

iii.

machine 2 is worse, increase MIPS to 667:

$$
MIPS_2 = 667 = \frac{1150M}{1M*CPI} \rightarrow CPI = 1.724
$$

$$
1.724 = X*0.6 + 2*0.3 + 5*0.1  \rightarrow X = 1.04
$$

### c)

Message Passing: Each processor has a private physical address space connected by the interconnection Network.

Shared Memory: Each processor may have their own private address space but they all connect to shared memory and I/O through the interconnection network. NUMA has private and shared memory, while UMA only contains shared memory. 

## B1

### a)

Virtual memory provides a contiguous addressing space to each process, which can be mapped to multiple fragmented blocks of available physical memory.

Increasing the addressing space available to a process beyond that which may be physically present in the RAM and simplifying memory management for tasks, enhancing security, minimising the risk of overflows affecting other processes.

### b)

i.

Temporal: Memory that is frequently accessed will be loaded into the cache after the first miss, greatly reducing the miss rate for repeated accesses. Caches store the most recently used memory of a given address, which in the case of an associative cache, will sometimes track the most recently accessed elements and keep them stored in the cache.

ii.

Spatial: Adjacent elements will be loaded in, depending on the block size, meaning that misses will be greatly reduced for contiguous arrays of memory. Blocks are typically larger than a single word, meaning that sequential elements of a contiguous array will likely result in hits after the initial compulsory misses.

### c)

i.

Block Number = 128

Block Size = 128B

Cache Size = 16KiB

Block offset bits = 7b

Index bits = 7b

Tag bits = 18b

ii.

Block offset bits = 7b

Index bits = 5b

Tag bits = 20b

hit time increases as there are more blocks to compare to

miss rate decreases as the increased associativity increases flexibility and reduces the chance that useful data is expelled from the cache

### d)

i.

Clock time = 1/2.9 = 344.8ps

hit time + miss penalty = 90ns = 261 cycles


miss_rate_i = 0.025, data_access= 0.25, miss_rate_d = 0.1

$$
CPI = 1 + 0.025*261 + 0.1*0.25*261 = 14.05
$$

ii.

L2 hit time = 5ns = 15 cycles

$$
CPI = 1 +  2*(L2MR*(0.025*(261+15)) + (1-L2MR)*(0.025*15)) = 7
$$

$$
(L2MR*(0.025*(261+15)) + (-L2MR)*(0.025*15)) = 3 - 0.025*15
$$

$$
(L2MR*(0.025*(261+15)) + (-L2MR)*(0.025*15)) = 2.625
$$

$$
L2MR*(0.025*(261))  = 2.625
$$

L2MR = 0.4 = 40.2%

## B2

### c)

> bgt s1, t0, DONE

i.

Psedo-instructions provide syntactic sugar for the reader/writer of assembly. They are **not** implemented in hardware, rather they are translated into one or more hardware implemented instruction by the assembler.

bgt s1, t0, DONE can be implemented by blt t0,s1,DONE

DONE = PC + 8, decode 8 = 1000

rs2 = s1 = x9

rs1 = t0 = x5

0000 0000 1001 0010 1100 0100 0110 0011 -> 0x0092C463

ii.

kinda answered it above

### d)

i.

Base Addressing

Address generation is completed by sign extending the immediate(12:1 -> 31:0), using the ALU to sum rs1 to the immediate. Passing the result to the Data memory and using rs2 as the write data.

ii.

in the notes

## B3

### a)

i.

IF ID EXE MEM WB

ii.

1 + 32 + 32 + 32 = 97

### b)

1 stall - stall is required for the mem read as we need to wait for the load to finish if it's a static issue core.

Assume forwarding from any of EX, MEM, WB:

    lw  s0, 20(t1) IF   ID   EX   MEM  WB
    add t2, s0, t0      IF   ID   --   EX   MEM  WB 
    sub t4, t2, t3           IF   --   ID   EX   MEM  WB
    sw  t4, 20(t1)                --   IF   ID   EX   MEM  WB  

### c)

i.

200*7 = 1400ps

ii.

200*9 = 1800ps

### d)

i.

write register has not been propagated through the pipeline, so it will not reach the Reg file at the same time as the data and control signals, resulting in incorrect register writes

ii.

not drawing that - in the notes

add another 5bits so 97 + 5 = 102