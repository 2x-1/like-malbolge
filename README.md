# like-malbolge
A bit of an experiment of a 8080 like machine code language, with ideas taken from Malbolge
## Registers
* `PC` (16 bit): Initially 0, holds the address to the current program.
* `SP` (16 bit): Initially 65535, holds the address to the top of the stack.
* `A` and `F` (both 8 bit): The Accumulator and the Flags register. They can be used as `AF` combined for some ops.
* `D` and `E` (both 8 bit): Two 8 bit registers. They can be used as `DE` combined for some ops.
* `H` and `L` (both 8 bit): Maybe I can eliminate the use of them somehow

## Instruction decoding
Decoded as `(PC + [PC])%94`. Some instructions may take the literal value of `[PC]` as an immediate value. All codepoint values in `[0..255]` is allowed in a source program.

### Instruction set
The instructions set is intentionally kept very sparse to ease programming. All undefined ops are NOPs.

| (PC+[PC])%94 | Description |
| :----------: | :---------: |
|      8       |   A = [C]   |
|      78      | Halt the machine |
