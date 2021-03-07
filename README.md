# like-malbolge
A bit of an experiment of a 8080 like machine code language, with ideas taken from Malbolge
## Design goals
* The instructions should have as little side-effect as possible, to make it realistic to recover from instructions not supposed to be executed.
  * The side effects should be accessible, in order to make use of the current condition.

## Registers
* `C` (unbounded): Initially 0, holds the address to the current program.
* `SP` (unbounded): Holds the address to the top of the stack.
* `F` (8-bits): Holds the status for the previous operation modifying the flags.
* `A` (unbounded): Accumulator, for temprarily storing values

## Instruction decoding
Decoded as `(C + [C]) % 94`. Some instructions may take the literal value of `[C]` as an immediate value. All codepoint values in `[0..255]` is allowed in a source program.

### Instruction set
The instructions set is intentionally kept very sparse to ease programming. All undefined ops are NOPs.

|  (C+[C])%94  | Arguments | Description |
| :----------: | :-------: | :---------: |
|      8       |           |    A ++     |
|      10      |   a, b    |    a + b    |
|      20      |   a, b    |    a - b    |
|      25      |           |    A --     |
|      42      | | |
|      78      |           | Halt the machine |
|      81      |   a, b    |    a & [C]  |
|      92      |   a, b    |    a | [C]   |
