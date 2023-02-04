# Type System

Any kind of type definition is started with `type`

### Declarations

#### A Tag

The most simple kind of type is a tag, it does not store and data and may function merely as a trait.

``type AbstractTag``

#### Type as a Type Reference

Given other existing types, a new type can refer to another type with generics or as an array

```
type str = [char]
type IntVec = Vec<int>
```

#### Enumerables

```
type Enum (
    Member1 |
    Member2 |
    Member3 (str, uint)
)
```

#### Structures

```
type Structure (
    field1 uint,
    field2 str = "default value",
    field3 AnotherType
)
```

#### Tuples

```
type Tuple = (uint, str, bool)
type Vec3 = [int * 3]
```

#### Generics and Recursive Storage

```
type LinkedList <Type> (
    NodeEnd |
    NodeValue (
        value Type,
        before Option< LinkedList<Type> >,
        after Option< LinkedList<Type> >
    )
)

type Result <TOk, TErr> (
    Ok(TOk) |
    Err(TErr)
)

type OnlyOk <Content> = Result <Content, ()>

type Option <C> = (Null | Has(C))
```

#### Semantic Sugar: Option Shortcut

```
    be k int? = null # This is not 'null' like in other programming languages, but an unpacked enum member.
```

### Initialization

```
be s = Structure (
    field1 = 0,
    field3 = AnotherType.new()
)

be e = Enum.Member2
   e = Enum.Member3 ("Hello", 100)
   
be s str # Declaring variable without initializing
```

### Enum Unpacking

[Rust like flow control with enum](https://doc.rust-lang.org/rust-by-example/flow_control/if_let.html) is a must have!

```
if be Enum.Member3 (string_variable, numeric_variable) = e {
    # e is Enum.Member3 and variables can be used
}

if e {
    case Enum.Member3(string_variable, numeric_variable)
        # ...

    case Enum.Member2 | Enum.Member3
        # ...
}
```

## Methods

Types are declared in one place with their data, methods do not coexist in the same declaration but are added outside. The first thing to do is to navigate into the correct scope. Static functions are declared like regular `fn`s, dynamic methods require the `self` parameter as first argument

```
Type {
    fn this_is_static {
        # This method is static and requires no arguments
    }

    fn this_is_static_2 (i uint) {
        # This method is static and requires an unsigned integer argument
    }
    
    fn this_is_dynamic (self, i uint) {
        # This method is dynamic and requires an integer argument
    }
}

be k Type
Type.this_is_static()   # static function call
k.this_is_dynamic(5)    # dynamic method call
```

