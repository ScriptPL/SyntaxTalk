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

#### Unpacking Structures and Imports

be can also be used to destruct a complex value collection into pieces or getting certain values from imports.

```
be a, b, c, d = complex_structure
be func1, func2, constant1 = use 'module'
```

#### 'be' as in 'it shall be'

Keeping the idea of few keywords, minimalism, but a lot of functionality and syntactic sugar the second meaning after 'it can be' is 'it shall be' where compile time assertions are supported. Using `be: statement` it is made sure that at no cost an invalid parameter is given.

```
fn int_function (i uint) {
    be: i != 0
    ret 1 / i
}
```
