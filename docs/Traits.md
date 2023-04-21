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
