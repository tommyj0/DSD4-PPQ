# Digital System Design 4 2024

            addi x20, x18,0     // p = &A[0]
            addi x21, x19,-2    // x21 = size -2
            addi x21, x21, 2    // x21 = (size -2)*4
            add  x21, x21,2     // x21 = &A[size-2]
    START:  bge  x20, x21,DONE  // if p >= &A[size-2]
            lw   x24, 0(x20)    // x24 = *p
            lw   x23, 4(x20)    // x23 = *(p+1)
            not  x24, x24       // x24 = ~x24
            and  x23, x23, x24
            sw   x22, 8(x20)  
            addi x20, x20, 4
            j    START
    DONE: 

## A1