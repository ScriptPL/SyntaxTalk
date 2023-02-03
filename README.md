# SyntaxTalk

```py
# Very simple program
# to output prime numbers
# to console indefinitely.

fn main {
    be i = 2
    
    for {
        be isPrime = true
    
        for be j = i {
            if i %0 j {
                isPrime = false
            }
        }
        
        if isPrime : println (i + " is a prime!")
        
        i += 1
    }
}
```

The idea is to create a minimalist but powerful programming language.

# Ideas

- [`Lexer.........`](https://github.com/ScriptPL/SyntaxTalk/blob/main/docs/Lexer.md) 
