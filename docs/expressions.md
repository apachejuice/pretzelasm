# Expressions

## TOC
  - [Syntax](#syntax)
  - [Grammar](#grammar)

## Syntax
Expressions are used to create values. Such values can be strings, integers or floating-point numbers, and they are constant meaning all expressions are evaluated before any LLVM code.

Strings are UTF-32 strings, do note that escapes are **not** supported. Use expressions instead.

There are N types of operations available:
- Addition with the `+` operator
- Subtraction with the `-` operator
- Multiplication with the `*` operator
- Division with the `/` operator
- Parentheses to increase precedence
- Concatenation of strings (and UTF-32 integer values with strings) (space separated)

The following are all valid expressions:
- `'string value' 33` evaluates to `'string value!'` (33 is the value of `!` in UTF-32)
- `33 + 2` evaluates to `35`
- `33 - 2` evaluates to `31`
- `33 * 2` evaluates to `66`
- `33 / 2` evaluates to `16` (use `33.0 / 2` to create a floating-point value `16.5`)
- `(33 + 2) * 2` evaluates to `35 * 2` which evaluates to `70` (whereas in `33 + 2 * 2` the multiplication is evaluated first, which gives us `37`)

## Grammar
```bnf
expression ::= concatenation

concatenation ::= addition ( addition )*

addition ::= multiplication ( ( '+' | '-' ) multiplication )*

multiplication ::= atom ( ( '*' | '/' ) atom )*

atom ::= string | number | '(' expression ')'
```
