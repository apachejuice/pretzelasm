# Names

## TOC
  - [Syntax](#syntax)
  - [Grammar](#grammar)

## Syntax
Names are simple. There are two types: symbol literals and words. Words are simply identifiers conforming to the regex `[a-zA-Z_][a-zA-Z_0-9]*`. Symbol literals are nonempty strings inside backtics:
```
`a simple symbol literal`
```

## Grammar
```bnf
name ::= word | symbol_literal

word ::= [a-zA-Z_][a-zA-Z_0-9]*

symbol_literal ::= '`' .+ '`'
```
