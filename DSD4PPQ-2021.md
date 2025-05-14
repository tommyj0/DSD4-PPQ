# Digital System Design 4 2021

## A1

### a)

i.

$$
CPI = 0.15A + 0.4B + 0.15C + 0.3D
$$

$$
MIPS = \frac{CR}{1M*CPI}
$$

$$
\textrm{Execution Time } = \frac{IC}{MIPS}
$$

CPI1 = 2.15
CPI2 = 2.55
CPI3 = 2

MIPS1 = 1,395
MIPS2 = 1,333
MIPS3 = 1,250

Exe time 1 = 1.43ms
Exe time 2 = 1.5ms
Exe time 3 = 1.6ms

ii.

Slowest processor is P3

reduce the class D instruction, as it holds the highest weight. This represents Common case fast.

iii.

cba

### b)

assume that 0 is preloaded into t0/i

            addi t4, x0, 40
    START:  bge  t0, t4, DONE
            add  t1, s1, t0 // t1 = &A[i]
            lw   t1, 4(t1)  // t1 = A[i + 1]
            add  t2, s2, t0 // t2 = &B[i]
            lw   t2, 8(t2)  // t2 = B[i + 1]
            or   t2, t1, t2 // t2 = A[i + 1] | B[i + 1]
            not  t2, t2     // t2 = ~(A[i + 1] | B[i + 1])
            add  t1, s1, t0 // t1 = &A[i]
            lw   t1, 0(t1)  // t1 = A[i]
            sub  t1, t1, t2 // 
            add  t3, s3, t0 // t3 = &C[i]
            sw   t1, 0(t3)  // C[i] = t1
            addi t0, t0, 4  // i++
            j    START      // pseudo instr to jump to start 
    DONE:


## B1

### b)

i.

800ps*3 = 2400ps

## B2

### a)

i.

Cache Size = 1KiB

Block size = 16B

Block Offset = 4b

Block number = 1KiB/16B = 64

Index bits = 6b

Tag bits = 22b

ii.

| Byte Access | Tag | Index | Offset | Hit/Miss | Replaced | 
|---|---|---|---|---|---| 
| 0000 0100 | 00 | 000000 | 0100 | Miss | <0x00-0x0F> | 
| 0001 0000 | 00 | 000001 | 0000 | Miss | <0x10-0x1F> | 
| 0000 1100 | 00 | 000000 | 1100 | Hit  | <0x00-0x0F> | 
| 1011 0000 | 00 | 001011 | 0000 | Miss | <0xB0-0xBF> | 
| 1110 0100 | 00 | 001110 | 0100 | Miss | <0xE0-0xEF> | 
| 1001 1100 | 00 | 001001 | 1100 | Hit  | <0x90-0x9F> | 
| 0100 0000 1000 | 01 | 000000 | 1000 | Miss  | Replace <0x00-0x0F> | 
| 0001 1100 | 00 | 000001 | 1100 | Hit  | <0x10-0x1F> | 
| 1011 0100 | 00 | 001011 | 0100 | Hit  | <0xB0-0xBF> | 
| 1100 0001 1100 | 11 | 000001 | 1100 | Miss  | Replace <0x10-0x1F> | 
| 1001 0000 | 00 | 001001 | 0000 | Hit  | <0x90-0x9F> | 
| 1000 1000 1000 | 00 | 001000 | 1000 | Miss  | <0x80-0x8F> | 

iii.

won't be asked :)

### b)

i.

Assume the array is aligned to the block

The first access will trigger misses on both L1 and L2 caches.

subsequent accesses will result in an L1 hit.

ii.

for one thread:

$$
50*4*256 + 20*1024 + 400*1024 = 481,280ns
$$

iii.

Constant replacements in L2 cache, resulting in drastically worse performance. Could be fixed with greater associativity (2-way works for this problem).