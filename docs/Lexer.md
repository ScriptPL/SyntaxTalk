# Lexer

### Comments

- `// ... \n`
- `#  ... \n`
- `/* ... */`

### String Literals

- ` " ... " ` 
- ` ' ... ' `
- `` ` ... ` ``

#### Backtick String | Formatted String

```js
insertion = "syntactic sugar"
`Backtick strings allow ${insertion} for formatting.`
```

### Numerics

```py
505                         # Number              : can be parser to 64 bit architecture
-5.1                        # Non-Integer Numeric :
2184792173492134912342      # Numeric Token       : token as sequence of digits
1i                          # Complex Numeric     : numbers with character sequence after it 
100 000 000                 # Formatted Numeric   : formatted numbers
```

### Variables

Variables must start with a letter or underscore, followed by an optional sequence of several digit, letter or underscore characters. Underscore at the start of a variable refers a non visible attribute.

```
be variable = 0
be _hidden_attribute = "This is a private field."
```

### Primitive Types

```js
uint(64)
int
int(32)
unum
num
char
str // (= char[])
bool
byte
```

### Reserved Keywords

```py
use             # package management

fn              # universal declaration of code: first-class function, attributes, etc.
type            # universal structure/enum/type declaration
for, in, next   # repetetive control flow
ret             # return scope
if, el, case    # conditional control flow

throw           # throw an exception

be              # declaration, etc.
self            # recursive self or parent reference

true, false,    # values

T, _         # Type and null value
```
