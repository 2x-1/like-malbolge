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
The instructions set is intentionally kept very sparse to ease programming.
All undefined ops are NOPs, unless the -p flag is set, in which they raise a SIGILL error.

|  (C+[C])%94  | Arguments (discarded when used) | Description |
| :----------: | :-------: | :---------: |
|      8       |           |    A ++     |
|      10      |   a       |    A += a   |
|      20      |   a       |    A -= a   |
|      25      |           |    A --     |
|      30      |           |    push A   |
|      35      |           |   push [A]  |
|      36      |           |   push [C]  |
|      38      |           | Swap A with TOS |
|      42      |           | Officially defined NOP |
|      51      |           | If A == 0, C += signed [C] ord value |
|      55      |   a       | If A == a, C += signed [C] ord value |
|      65      |   a       | [A] = a     |
|      66      |           | push [A++]  |
|      67      |           | Repeat next instruction until TOS == 0 |
|      68      |           | A--. If A >= 0, C += signed [C] |
|      78      |           | Halt the machine |
|      81      |   a, b    |    a & [C]  |
|      88      |           |  A = SHL(A) |
|      89      |           |  A = ROL(A) |
|      92      |   a, b    |    a | [C]  |
