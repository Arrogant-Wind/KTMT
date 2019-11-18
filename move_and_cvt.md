# FP Load and Store


        # MIPS
        #
        # Load word in to coprocessor 1
        lwc1 $f0, 4($t4)   #  $f0 = Mem[ $t4 + 4 ]

        #
        # Load double in to coprocessor 1
        ldc1 $f0, 0($t4)   #  $f0 = Mem[ $t4 + 0 ];  $f1 = Mem[ $t4 + 4 ]
        #
        # Store word from coprocessor 1.
        swc1 $f0, 4($t4)   #  $f0 = Mem[ $t4 + 4 ]
        #
        # Store double from coprocessor 1.
        sdc1 $f0, 0($t4)   #  Mem[ $t4 + 0 ] = $f0;  Mem[ $t4 + 4 ] = $f1


 # Move Instructions

        # MIPS
        #
        # Move to coprocessor 1
        mtc1 $t0, $f0      # f0 = t0   Note that destination is *second* reg.
        #
        # Move from coprocessor 1.
        mfc1 $t0, $f0


 # Data Type Conversion

        # Convert between floating-point and integer formats.
        # NOTE: Values don't convert automatically, need to use these insn.

        # MIPS
        #
        # To: s, d, w;  From: s, d, w
        #
        # cvt.TO.FROM fd, fs
        #
        cvt.d.w $f0, $f2     # $f0 = convert_from_int_to_double( $f2 )
        

 # Setting Condition Codes
        # In preparation for a branch, set cond code based on FP comparison.

        # MIPS
        #
        # Compare:   fs COND ft
        # COND: eq, gt, lt, le, ge
        # FMT: s, d
        #
        # c.COND.FMT fs, ft
        # Sets condition code to true or false.
        # Condition is false if either operand is not a number.
        #
        c.lt.d $f0, $f2    # CC = $f0 < $f2
        bc1t TARG          # Branch if $f0 < $f2
        nop
        c.ge.d $f0, $f2    # CC = $f0 >= $f2
        bc1t TARG2          # Branch if $f0 < $f2
        nop
        # Reachable?
        Instruction	Operation
        c.eq.d	Fs1, Fs2	set floating point coprocessor flag true if equal double  
        c.eq.s	Fs1, Fs2	set floating point coprocessor flag true if equal float  
        c.ge.d	Fs1, Fs2	set floating point coprocessor flag true if greater or equal double  
        c.ge.s	Fs1, Fs2	set floating point coprocessor flag true if greater or equal float  
        c.gt.d	Fs1, Fs2	set floating point coprocessor flag true if greater than double  
        c.gt.s	Fs1, Fs2	set floating point coprocessor flag true if greater than float  
        c.le.d	Fs1, Fs2	set floating point coprocessor flag true if less or equal double  
        c.le.s	Fs1, Fs2	set floating point coprocessor flag true if less or equal float  
        c.lt.d	Fs1, Fs2	set floating point coprocessor flag true if less than double  
        c.lt.s	Fs1, Fs2	set floating point coprocessor flag true if less than float  
        c.ne.d	Fs1, Fs2	set floating point coprocessor flag true if not equal double
        c.ne.s	Fs1, Fs2	set floating point coprocessor flag true if not equal float

 # FP Branches

        l.s     $f0,A
        l.s     $f2,B
        
        c.lt.s  $f0,$f2          # is A < B?
        bc1t    printA           # yes -- print A
        c.lt.s  $f2,$f0          # is B < A?
        bc1t    printB           # yes -- print B
  
  # Example
```## min.asm --- determine the min of two floats
##
        .text
        .globl main

main:   # get the values into registers
        l.s     $f0,A
        l.s     $f2,B
        
        c.lt.s  $f0,$f2          # is A < B?
        bc1t    printA           # yes -- print A
        c.lt.s  $f2,$f0          # is B < A?
        bc1t    printB           # yes -- print B

        la      $a0,EQmsg        # otherwise
        li      $v0,4            # they are equal
        syscall
        mov.s   $f12,$f0         # print one of them
        b       prtnum
        
printA: la      $a0,Amsg         # message for A
        li      $v0,4
        syscall
        mov.s   $f12,$f0         # print A
        b       prtnum
        
printB: la      $a0,Bmsg         # message for B
        li      $v0,4
        syscall
        mov.s   $f12,$f2         # print B
        
prtnum: li      $v0,2            # print single precision
                                 # value in $f12
        syscall
        la      $a0,newl
        li      $v0,4            # print new line
        syscall
        jr      $ra              # return to OS

        .data

A:      .float  4.830
B:      .float  1.012
Amsg:   .asciiz "A is smallest: "
Bmsg:   .asciiz "B is smallest: "
EQmsg:  .asciiz "They are equal: "
newl:   .asciiz "\n"
       
        ```
