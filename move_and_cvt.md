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


 # FP Branches

        # MIPS
        #
        # Branch insn specifies whether CC register true or false.
        #
        bc1t TARG
        nop
        #
        bc1f TARG
        nop
