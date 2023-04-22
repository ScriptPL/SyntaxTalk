# SyntaxTalk

```py
# Very simple program
# to output prime numbers
# to console indefinitely.

fn main {
    be i = 2
    
    for {
        be isPrime = true
    
        for<l> be j = 2 <= ... < sqrt(i) {
            if i %0 j {
                isPrime = false
                ret<l>
            }
        }
        
        if isPrime : println (i + " is a prime!")
        
        i += 1
    }
}
```

The idea is to create a minimalist but powerful programming language.

# Ideas

- [`Lexer...................`](https://github.com/ScriptPL/SyntaxTalk/blob/main/docs/Lexer.md) All ideas regarding the lexer (string to token converter of the programming language)
- [`Control Flow............`](https://github.com/ScriptPL/SyntaxTalk/blob/main/docs/ControlFlow.md) All 'basics' like if's and loop's
- [`Types...................`](https://github.com/ScriptPL/SyntaxTalk/blob/main/docs/Types.md) Type System and structs
