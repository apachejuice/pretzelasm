# Types

## TOC
  - [Syntax](#syntax)
  - [List of value types](#list-of-value-types)
  - [Implementation details](#implementation-details)
  - [Grammar](#grammar)

## Syntax
Types are defined by their category. There are five categories of types that are defined by their first character:
- Reference types, start with the `$` character followed by a relative path: `$std/String`.
- Array types, start with the `[` character followed by any type followed by a `]`.
- Sized array types, starting with the `*` character followed by a numeric size and an array type: `*5[$std/String]`
- User-defined value types, aka structs, start with the `#` character followed by a path: `#std/net/IP6Packet`.
- Built-in value types, starting with any other character than `$`, `#` or `[`: `i32`, `char`, `bool`.

An `!` is also a type denoting an empty return value. It is however not listed here as it compiles down to the LLVM type `void`.

## List of value types
| Name 	| Type           	| Size     	| Signedness 	| Description                                  	|
|------	|----------------	|----------	|------------	|----------------------------------------------	|
| i8   	| integer        	| 8 bits   	| signed     	| 8-bit signed integer type, 2's complement    	|
| i16  	| integer        	| 16 bits  	| signed     	| 16-bit signed integer type, 2's complement   	|
| i32  	| integer        	| 32 bits  	| signed     	| 32-bit signed integer type, 2's complement   	|
| i64  	| integer        	| 64 bits  	| signed     	| 64-bit signed integer type, 2's complement   	|
| u8   	| integer        	| 8 bits   	| unsigned   	| 8-bit unsigned integer type, 2's complement  	|
| u16  	| integer        	| 16 bits  	| unsigned   	| 16-bit unsigned integer type, 2's complement 	|
| u32  	| integer        	| 32 bits  	| unsigned   	| 32-bit unsigned integer type, 2's complement 	|
| u64  	| integer        	| 64 bits  	| unsigned   	| 64-bit unsigned integer type, 2's complement 	|
| f32  	| floating point 	| 32 bits  	| signed     	| 32-bit signed floating-point type            	|
| f64  	| floating point 	| 64 bits  	| signed     	| 64-bit signed floating-point type            	|
| f128 	| floating point 	| 128 bits 	| signed     	| 128-bit signed floating-point type           	|
| char 	| character      	| 32 bits  	| signed     	| 32-bit UTF-32 character                      	|
| bool 	| boolean        	| 1 byte   	| -          	| Boolean type holding a true or a false       	|

## Implementation details
- Boolean arrays and sized boolean arrays may be stored as an integer of required length to save space (dependent on target machine word size), for example:
    - `*n[bool]` may be turned to `ix` where `x >= n >= 2`
    - `[bool]` may be turned into any integer value depending on size

## Grammar
```bnf
type ::= '!' | reference_type | array_type | sized_array_type | user_defined_value_type | built_in_type

reference_type ::= '$' qualified_reference

qualified_reference ::= name ( '/' name )*

array_type ::= '[' type ']'

sized_array_type ::= '*' number array_type

user_defined_value_type ::= '#' qualified_reference

built_in_type ::=
    'i8'    |
    'i16'   |
    'i32'   |
    'i64'   |
    'u8'    |
    'u16'   |
    'u32'   |
    'u64'   |
    'f32'   |
    'f64'   |
    'f128'  |
    'char'  |
    'bool'
```
