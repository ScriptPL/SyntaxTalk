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

#### Length

```
type fn Length {
    fn len(self) -> uint
}
```

#### Iter

```
type fn Iter<T> {
    fn next(self) -> Opt<T>
}
```

#### Backwards Iter

```
type fn IterLeft<T> {
    fn back(self) -> Opt<T>
}
```

#### PosIter

```
type fn IterState<T> use Iter<T> {
    fn has_next(self) -> bool
}
```

#### Indexable

```
type fn Index<T> use Length, IterState<T> {
    fn 'index' (self, int) -> Opt<T>
}
```

#### Push

```
type fn Push<T> use Index<T> {
    fn push (self, T) -> bool
}
```

#### Pop

```
type fn Pop<T> use Index<T> {
    fn pop (self) -> T
}
```

#### Push Left

```
type fn PushLeft<T> use Index<T> {
    fn pushl (self, T) -> bool
}
```

#### Pop Left

```
type fn PopLeft<T> use Index<T> {
    fn popl (self) -> T
}
```
