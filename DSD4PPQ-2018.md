# Digital System Design 4 2018

## A1

### a)

The development of transistors has greatly reduced the gate size, allowing more and more transistors to be packed into modern processors. This rapid advancements in transistor count and computation is described by Moore's Law.

Vacuum Tubes Triodes were used before transistors. They were significantly slower, unreliable and less efficient. They can still be seen in some modern guitar amplifiers due to their supposedly warmer sonic characteristics.

### b)

The increase in market share for RISC computers, when compared to CISC computers is due to the rise of mobile and embedded devices which are more catered to executing many simple instructions, rather than the few complicated ones found in CISC computing. The popularity of ARM is also an important factor in the recent rise of RISC computing, due to their extensive line of RISC cores and open licensing.

### c)

Structural: Usually referring to the VN bottleneck, structural hazards are characteristics of the CPU architecture that prevent certain pipeline stages from being executed simultaneously.

Control: Conditional branches may stall the pipeline as the next instruction cannot be fetched until the branch outcome has been found. The stalls can be minimised with speculation, which can either be static or dynamic.

Data: Data hazards occur when the result of a previous instruction is required before the operation has been completed. This can be resolved by forwarding and/or reordering.

### d)

Pseudo-instructions provide syntactic sugar to the reader/programmer, abstracting commonly used operation, such as mv x1,x2 into their hardware implementations: addi x1,x2,0

### e)

i.

$$
CPI_{1} = 0.6*1 + 0.3*2 + 0.1*4 = 1.6
$$

$$
CPI_{1} = 0.6*2 + 0.3*3 + 0.1*4 = 2.5
$$

ii.

$$
MIPS_{1} = \frac{CR_1}{10^6*CPI_1} = \frac{800M}{1M*1.6} = 500 MIPS
$$

$$
MIPS_{2} = \frac{CR_2}{10^6*CPI_2} = \frac{1000M}{1M*2.5} = 400 MIPS
$$

iii.

M2 has lower mips, largest cycles per instruction class is class A. First, finding required CPI change to reach 500 MIPS:

$$
CPI_2 = \frac{CR_2}{10^6*MIPS_2} = \frac{1000M}{1M*500} = 2
$$

$$
CPI_2 = X*0.6 + 0.3*3 + 0.1*4 = 2
$$

$$
X = \frac{2-0.3*3 -0.1*4}{0.6} = 1.17
$$

iv.

performance change is 500/400 = 1.25x speedup.

This is representative of making the common case fast. The highest frequency instruction class would require the least relative improvement.

### f)

A speculation vulnerability allowing a process to read all memory in a given system