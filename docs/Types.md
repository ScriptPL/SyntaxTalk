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
    Member3 (str, usize)
)
```

#### Structures

```
type Structure (
    field1 usize,
    field2 str = "default value",
    field3 AnotherType
)
```

#### Tuples

```
type Tuple = (usize, str, bool)
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
    Ok(TOk),
    Err(TErr)
)

type Option <Content> = Result <Content, ()>
```
