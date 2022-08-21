# Functions

## TOC
  - [Syntax](#syntax)
  - [The function body](#the-function-body)
    - [Instructions](#instructions)
    - [Labels](#labels)
    - [Line metadata](#line-metadata)
  - [Grammar](#grammar)

## Syntax
Functions in PretzelASM are declared with the keyword `func` preceeded by a dot. Below is an example function declaration with the signature `([String]) Int`:
```py
.func main ([$std/String]) i32
    # function body
.end
```

A function declaration starts with a dot followed by `func`, the name of the function (see [`names.md`](./names.md)) and a list of arguments in parentheses, following a type representing the return type. The special type `!` denotes no return value (see [`types.md`](./types.md)).

The return type is then followed by an arbitrary (at least 1) number of newlines and semicolons, referred to as a separator. A function ends with a separator, a dot, and the keyword `end`.

## The function body
A function body consists of a header, and any number of the following three things:
- Labels
- Instructions
- Line metadata

Only instructions are required to create a function, but line metadata is often included to help with debugging, and labels are mainly used for loops.

### Instructions
See `instructions.md`.

### Labels
A label consists of a colon, followed by a valid name:

`:some_label`

Labels can be jumped to using the `jump_*` family of instructions.

### Line metadata
Line metadata simply associates instructions with line numbers. They are declared using the `%` character followed by the given instruction, and the instructions after that are interpreted to be on the same line until the following line metadata:
```py
%1 create_object [$some/library/SomeClass] # on line 1
call_method ' ' '()!' [] # call the empty method (constructor) with signature ()! and no arguments
%2 call_method 'some_method' '()!' [] # not on line 1 anymore, but 2
```
The signature `()!` denotes a method that takes no arguments and has no return value.

## Grammar
```bnf
function ::= '.' 'func' name args_list separator function_body separator '.' 'end'

args_list ::= '(' type* ')' type

function_body ::= ( ( instruction | label ) separator )+

label ::= ':' name

instruction ::= line_meta? opcode argument*

line_meta ::= '%' number
```
