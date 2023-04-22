# Traits

A trait is a collection of methods that are assigned to a type, for simplicity, the declarative keyword is `type fn`: A collection of functions for a type

```
type fn Trait {
    fn dynamic_method(self, usize, str)
    fn dynamic_method_without_args(self)
    fn traits_can_also_have_static_functions()
}
```

### Implementing Trait for a Type

A type 'implements' a trait or it simply **uses** that behaviour.

```
Type use Trait {
    fn dynamic_method(self, usize, str) {
        ...
    }
    
    fn dynamic_method_without_args (self) {
        ...
    }
}
```

## Std-Lib Trait Hierarchy

### Collection/ Set

```
type fn Length {
    fn len(self) -> uint
}

type fn Index<T> use Length, IterState<T> {
    fn 'index' (self, int) -> Opt<T>
}
```

#### Iter

```
type fn Next<T> {
    fn next(self) -> Opt<T>
}

type fn HasNext<T> {
    fn has_next(self) -> bool
}

# Backwards Iterator

type fn Back<T> {
    fn back(self) -> Opt<T>
}


type fn HasBack<T> {
    fn has_back(self) -> bool
}
```

#### Queue

```
type fn PushRight<T> use Index<T> {
    fn pushr (self, T) -> bool
}

type fn PopRight<T> use Index<T> {
    fn popr (self) -> T
}

type fn PushLeft<T> use Index<T> {
    fn pushl (self, T) -> bool
}

type fn PopLeft<T> use Index<T> {
    fn popl (self) -> T
}
```
