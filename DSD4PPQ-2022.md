# Digital System Design 4 2022

## A1

### a)

i.

IC = 40 + 120 + 90 + 15 = 265

$$
CPI = \frac{2*40 + 120 + 5*90 + 2*15}{265} = 2.57
$$

$$
MIPS = \frac{CR}{1M*CPI} = \frac{2000M}{1M*2.57} = 778 \textrm{ MIPS}
$$

ii.

Double speedup = double CPI, FP ops don't carry half the CPI so it's not possible

iii.

$$
CPI = \frac{2*40 + 120 + X*90 + 2*15}{265} = 2.57/2
$$

$$
X = \frac{1.285*265 - 80 - 120 - 30}{90} = 1.228
$$

iv. 

Amdahl's Law

Total speedup can only be affected by the improvable part of the workload

v.

IC = 265

$$
CPI = \frac{2*40 + 120 + 6*90 + 4*15}{265} = 3.02
$$

$$
MIPS = \frac{CR}{1M*CPI} = \frac{3000M}{1M*3.02} = 993.4 \textrm{ MIPS}
$$

MIPS is higher for this processor.

In this case, where processors share the same ISA, MIPS is a relevant metric as instructions executed per second relates directly to performance. In a case where different ISAs were used, MIPS would be less relevant as different instructions could perform different tasks so the size of a program would have to be taken into account to find execution time.

Speedup = 993.4/778 = 1.28x

### b)

    // t0 = i
    // s0 = &A[0]
    // t1 = 4
    // t2 = A[i + 1]
    // t3 = A[i]
    // t4 = i*4
            addi t1, x0, 4      // t1 = 4
    START:  bge  t0, t1, DONE   // if i >= 4: finish
            add  t4, s0, t0     // t4 = &A[i]
            lw   t3, 0(t4)      // t3 = A[i]
            slli t3, t3, 3      // t3 = A[i] << 3
            not  t3, t3         // t3 = ~(A[i]<<3)
            lw   t2, 4(t4)      // t2 = A[i + 1]
            add  t2, t2, t3     // t2 = ~(A[i]<<3) + A[i + 1]
            sw   t2, 0(t4)      // A[i] = ~(A[i]<<3) + A[i + 1]
            addi t0, t0, 4      // i++
            j START
    DONE:

A[i] = -65 + 16 = -49

## B1

### b)

i.

2b, need to specify instruction format, lw/sw, beq or R-type

## B2

### a)

i.

Block size = 128B

Block Number = 512

Cache size = 64KiB

Tag bits = 16

Assume Write-Through scheme

Extra storage = 1b + 16b = 17b

Total Extra Storage = 17b*512 = 8704b = 1088B

ii.

Decrease Capacity misses, Locality can be better exploited for large data that would experience

15b,10b,7b

iii.

16b,8b,8b

misses are halved for sequential reads. Reduces compulsory misses, hit times are increased. 

iv.

17b,8b,7b

Conflict misses are decreased

### b)

i.

Arithmetic intensity is the number of Floating Point operations per the number of bytes that need to be stored/loaded. The graph represents the two bottlenecks of a multiprocessor system, either the memory bandwidth maintaining a constant ratio between FLOPs completed and FLOPs loaded creating the sloped region, or the floating point capabilities of the processor, the flat region.

ii.

no