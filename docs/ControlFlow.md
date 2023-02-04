# Control Flow

### Imports and Package Managing

Keeping minimalist standarts, the only keyword for importats is `use` which is followed by a string literal tracking the name of the package or file. The Lexer automatically scans for the keyword and starts lexing packages before the entry file is finished lexing.

```
# Import Libraries
use 'html', 'ecs', 'stdlib'

# Import your own files
use 'path/to/file.scriptpl'

# Import 3rd party
use 'www.link-to-repo.com/path/to/.git'
```

### Variables and Scopes

As an alternative to three character declarations like `let` and `var`, `be` only focuses on using two characters for extra laziness. `be` derived from 'to be' makes a variable 'be', as in exist. The declaration format is `be name type` and initialization format is `be name [type] = value` where the content in square brackets is optional.

```
be variable uint = 0
be number = 77
be casted = uint 0
```

The keyword `self` is used to refer to the self scope. For types it represents a function like `this` in Java and JavaScript, etc.

#### Unpacking Structures and Imports

be can also be used to destruct a complex value collection into pieces or getting certain values from imports.

```
be a, b, c, d = complex_structure
be func1, func2, constant1 = use 'module'
```

#### 'be' as in 'it shall be'

Keeping the idea of few keywords, minimalism, but a lot of functionality and syntactic sugar the second meaning after 'it can be' is 'it shall be' where compile time assertions are supported. Using `be: statement [, compile_error_message]` it is made sure that at no cost an invalid parameter is given, optionally followed by an error message.

```
fn int_function (i num) -> num {
    be: i != 0, "cannot divide by zero"
    
    ret 1 / i
}
```

## Functions

Functions are blocks of logic that can be automated to act in a certain order. All functions, unless lambdas, are declared with the `fn` keyword. A function is automatically exited at the end of its' scope or earlier with the `ret` keyword. Functions without parameters can leave out the round brackets such is the case of `fn main { ... }`

```
fn is_divisible (dividend uint, divisor uint) -> bool {
    be: divisor != 0, "cannot divide by zero"

    if dividend % divisor == 0 {
        ret true
    }
    
    ret false
}
```

To keep things small and clean, a function with one line of code is [Rust](https://www.rust-lang.org/)-like automatically executing the line as a return value

```
fn sum (num1 int, num2 int) -> int {
    num1 + num2
}
```

#### Lambdas

Lambdas are annotated with `=>`, a basic example would be `i => 2 * i`, thought it needs to be said that scopes annotated with fn can also be used as lambdas `fn (i) {2 * i}`

## Conditionals and Loops

Conditionals are boolean type operations that can be used to jump between blocks. Three keywords are of most importance to conditional jumps: `if`, `el`, `case`. Loops are cycles in a graph, but in programming it is an indicator of repeat code execution. The main keywords here are `for`, `in` and `next`. Both can be put together into one logic block, however the document will first take a look at separated behaviour.

### Conditionals

```
if stmt {
    ...
} el if stmt {
    ...
} el if stmt {
    ...
} el {
    ...
}
```

#### Comparators

The language should support special nests of comparison operators, it is semantically correct to say that `0 < x < 10` implies that x is in an exclusive range from 0 to 10, so it should also be syntactically valid. Additionally, supporting transitivity, mathematically speaking `a = b = c` is equivalent to `a = b` and `b = c` and `a = c`. This is the case for `<`, `<=`, `>`, `==`, `>=`, `!=` and like in other programming languages `&&` and `||`

```
0 <= rng < 10
val1 == val2 == val3
x > y
z <= 0
a && b && c
l1 || l2
```

#### 'in' as a preposition

`x in y` can be interpreted like a function `in(x, y)` and overriden. Such is the case for types `[str] in [str]` for contains substring, `[T] in [array of T]` for contains element, range detection like `num in range` for finding if an element is part of range, or the classic `variable in Trait` to see wether the variable is part of a certain trait logic.
X has to be a constant and not declared using `be` for ambigiouty between ['in' as in 'for ... in ...'](#in-as-in-for--in-)

```
'Hello' in 'Hello, World!'  # true
'Hi!' in 'Hello, World!'    # false
```

#### Switches

The language should support switch statements by declaring `case`s within an if block. To declare a constant case, use `case x`, to nest several constants use the vertical bar for separation `case 0 | 1 | 5` or start writing logic with in brackets: `case 0 | (x > 10)`

```
if value {
    case condition
        # code
    case condition1
        # code
} el {
    # not case
}
```

```
fn fibonacci (x uint) {
    if x {
        case 0 | 1
            ret 1
    } el {
        ret self (x - 1)        # self is equal to `fibonacci` here
    }
}
```

### Loops

#### Traditional For Loop

```
for be i = 0; i < 10: i += 1 {
    # loop from i = 0 to i = 9
}
```

The shortcut for this particular for loop would be `for be i = 9` which loops from `0` to `9` inclusively. If the variable is irrelevant you can skip the declaration part and specify how many iterations should execute `for 10`

#### While Loop

```
for condition {
    # while condition
}
```

A while loop is a started by writing a condition after the `for` keyword. To loop indefinitely, you can skip the condition part and just write `for { ... }`

#### 'in' as in 'for ... in ...'

Provided an iterable, we can quickly navigate through it with the statement `for be ... in iterable`.

#### Labels, Continue and Break

To identify which loop should be changed, a loop has to be assigned a label in the format `for <label> ...`. To jump to the next iteration, you would then use `next <label>`, to break the current iteration you would "return" form it with `ret <label>`

### Combined Logic Blocks

Python like nesting of _conditional_ loops and conditions should be supported:

```
for condition {
    # if you land here you get at least one iteration
} el {
    # if you land here you got zero iterations (condition was false from the very beginning)
}

if condition {
    # if true
} el for {
    # if false
}

for condition {
    # ...
} el if condition1 {
    # ...
} el for condition2 {
    # ...
}
```
