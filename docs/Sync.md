# Synchronous and Asynchronous programming.

`sync` is the leading keyword for synchronized programming while `!sync` (not sync) will be used as an asynchronous marker.

### Volatile variables

```
# Variables which fulfill atomic operations
sync be i = 0

# fn '+' >>> becomes >>> sync fn '+'
```

### A Promise

```
Promise {
    fn await () -> Result<T, E>
}
```

### Asynchronous function

```
use 'Thread'

!sync async_function () -> 1 {
    Thread.sleep(1000)
    ret 1
}

be i = async_function()
println("a")            # a
println(i.await().ok()) # 1
println("b")            # b
```

The `throw` keyword will automatically end a promise and pass by the error.

### Synchronized Functions

```
# Read Synchronization
fn synchronized_read_method(sync <R> self) -> int {
    ...
}

# Write Synchronization
fn synchronized_method(sync <RW> self, t int) {
    ...
}

# Synchronization
fn static_function(...) {
    ...
    
    sync <RW> var1, <R> var2, ... {
        ...
    }
    
    ...
}
```
