# like-malbolge
A bit of an experiment of a 8080 like machine code language, with ideas taken from Malbolge
## Registers
* `PC` (unbounded): Initially 0, holds the address to the current program.
* `SP` (unbounded): Holds the address to the top of the stack.
* `F` (8-bits): Holds the status for the previous operation modifying the flags.
* `A` (unbounded): Accumulator, for temprarily storing values

## Instruction decoding
Decoded as `(PC + [PC]) % 94`. Some instructions may take the literal value of `[PC]` as an immediate value. All codepoint values in `[0..255]` is allowed in a source program.

### Instruction set
The instructions set is intentionally kept very sparse to ease programming. All undefined ops are NOPs.

Most, if not all, instructions operate on the stack.

| (PC+[PC])%94 | Arguments | Description |
| :----------: | :-------: | :---------: |
|      8       |           |  B = [C]    |
|      10      |           |   B --      |
|      20      |           |             |
|      25      |           |   B ++      |
|      78      |           | Halt the machine |
|      81      |           |   B += [C]  |
|      92      |           |   B -= [C]  |
