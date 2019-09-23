The thing about computers is that they are made of a bunch of smaller computers.

I can even apply this idea down to things like registers.
A register can be thought of as having a set of opcodes for example:
    * nop, drive, load, reset; or
    * nop, drive, load, increment, reset

I think if I group the control signals into each component together into a single bus, as I do with all the data signals, I'll have better control over what exactly is going on.

The thing is, if I want only one register to be driven to a bus at a time, then it might make more sense for the main control bus to smimply index a register.
Which means the internals of the register will require a decoder (address recognizer) in order to translate the main bus control into register opcodes.