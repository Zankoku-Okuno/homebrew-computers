operation operand... conditional(condSrc condTest nextInstr operation operand...)


Offsets and immediate operands are interesting because they come in several sizes.
    * bit-index: the number of bits needed to encode any bit index within the largest code or data words
    * code-bits: the number of bits needed to encode any address into code memory
    * addr-bits: the number of bits needed to encode any address into data memory

As it happens, most of the time an entire code-bits or addr-bits operand is not needed.
Almost all data literals need 13 or fewer bits.
Most jumps are to nearby sections of code.
Thus, we should really decide on two sizes of immediate:
    * small numbers that cover the majority of cases
    * full-size numbers, and how to synthesize them if there's no direct encoding.



* Code
    * Absolute
        * can only be re-located by a linker
        * useful for larger jumps, as between libraries
    * PC-relative
        * useful for relocatable code without a linker (position-independent code)
        * small offsets, within a function or library
    * Register indirect
        * jump to a location only known dynamically
        * return from subroutine
        * switch tables
        * call through function pointers (a.k.a. virtual functions)
* Data
    * Register
        * normal scalars, operated on independently
    * Base plus offset (displacement)
        * access within a stack frame
        * accessing subfields in a large object
        * this covers register indirect when offset is zero
    * Immediate
        * almost all immediates fit in 13 bits
        * large contants could be loaded in several ways:
            * load half the constant, then the other half into the high half of the register
            * load PC-relative data
            * load the next word from the PC (and increment over the data)

Advanced Modes
    * Code
        * Conditional Execution
            * unless used to condition a jump, could avoid a pipeline flush
        * Skip instructions
            * skipping over an unconditional jump may as well just be a normal conditional jump
            * I'm not sure where this will really come in handy
    * Data
        * Absolute
            * useful for accessing shared global scalars as might be present in OSes
        * Indexed absolute (optionally scaled index)
            * useful for indexing into shared global arrays
        * Base plus (optionally scaled) index (optionally plus offset)
            * base and index are strored in registers
            * useful in the same way as base plus offset, but for arrays rather than scalars
        * Autoincr/autodecr register indirect
            * useful for array traversal as base plus index
            * the icr/decr side-effect can cause problems when recovering from interrupts
    * Memory indirect
        * added onto any other mode, load the real data from the specified location in memory
        * useful for pointer chasing, but obviously requires an extra memory access




