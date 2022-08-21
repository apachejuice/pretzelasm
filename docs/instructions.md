# Instructions

## TOC
  - [Syntax](#syntax)
  - [Arguments](#arguments)

## Syntax
An instruction consists of a possible line directive, the opcode label and arguments, if any. The following is an instruction with 3 arguments and a line directive:
```py
%1 call_method ' ' '()!' []
```
The following is an instruction with 1 argument and no line directive:
```py
i32push 0x123
```
The following is an instruction with no arguments or line directives:
```py
pop
```

The name of the instruction, i.e. the action, is called an *opcode*, in these cases `call_method`, `i32push` and `pop`.

## Arguments
Instruction arguments can be of 4 types:
- Expressions enclosed in brackets, see [`expressions.md`](./expressions.md): `{'this is a string ending with a newline' 0x10}`
- Integers in decimal, binary or hexadecimal: `123`, `0b0100101001`, `0x352D`
- String literals. Note that escapes aren't supported; to include such characters, use expressions.
- Lists of 0 or more elements of any other argument type enclosed in brackets: `[@someString, 0x00]`

## List of opcodes
A comprehensive list of the opcodes available for instructions, with detailed description and usage.

- [Integer operations](#integer-operations)
  - [32-bit signed](#32-bit-signed)

## Integer operations
## 32-bit signed
<hr>

### `i32push <integer>`
Description: Pushes a 32-bit integer onto the stack

Arguments:
  - `<integer>`: Any 32-bit integer value or expression evaluating to such.

Side effects: Stack grows by 1 item

Requirements: -

Example: `i32push 0x123`
<hr>

### `i32add`
Description: Adds two 32-bit integers from the stack

Arguments: -

Side effects: Stack shrinks by one item

Requirements: 2 32-bit integers on top of the stack

Example: `i32add`
<hr>

### `i32ret`
Description: Returns the top integer from the stack

Arguments: -

Side effects: Current function ends

Requirements: 1 32-bit integer on the top of the stack

Example: `i32ret`


